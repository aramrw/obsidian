#shaders #computer_graphics #calculus #algebra #geometry #trigonometry 

### [[Cube Shader]]

--- 

#### https://en.wikipedia.org/wiki/Ray_marching

> **Ray marching** is a class of rendering methods for [3D computer graphics](https://en.wikipedia.org/wiki/3D_computer_graphics "3D computer graphics") where [rays](https://en.wikipedia.org/wiki/Ray_\(optics\) "Ray (optics)") are traversed iteratively, effectively dividing each ray into smaller ray segments, sampling some function at each step. For example, in [volume ray casting](https://en.wikipedia.org/wiki/Volume_ray_casting "Volume ray casting") the function would access data points from a 3D scan. In Sphere tracing, the function estimates a distance to step next. Ray marching is also used in physics simulations as an alternative to [ray tracing](https://en.wikipedia.org/wiki/Ray_tracing_\(physics\) "Ray tracing (physics)") where analytic solutions of the trajectories of light or sound waves are solved. Ray marching for computer graphics often takes advantage of [SDFs](https://en.wikipedia.org/wiki/Signed_distance_function "Signed distance function") to determine a maximum safe step-size, while this is less common in physics simulations a similar adaptive step method can be achieved using adaptive [Runge-Kutta](https://en.wikipedia.org/wiki/Runge%E2%80%93Kutta_methods "Runge–Kutta methods") methods.

> The technique dates back to at least the 1980s; the 1989 paper "Hypertexture"[[1]](https://en.wikipedia.org/wiki/Ray_marching#cite_note-1) by [Ken Perlin](https://en.wikipedia.org/wiki/Ken_Perlin "Ken Perlin") contains an early example of a ray marching method.

--- 

# Implementation Details

### Positions

The full equation to calculate the position of the ray at any given step is:

```glsl
vec3 rayOrigin = vec3(0.0, 0.0, 3.0);
vec3 rayDirection = normalize(vec3(st.x, st.y, -1.0));
float totalDistance = 0.0;

for (int i = 0; i < 64; i++) {
	vec3 currentPos = rayOrigin + rayDirection * totalDistance;
}
```

$$v_{\text{current}} = v_{\text{origin}} + (v_{\text{direction}} \times d_{\text{total}})$$

#### Explanation 

Before adding the $v_{\text{origin}}$, the $v_{\text{dir}}$ must be scaled.

- `rayDirection` is a **[[Normalization|Normalized Vector]]** (typically by normalizing the screen coordinates relative to a camera look-at vector). 
- Because its length is `1.0`, it acts as a pure indicator of direction.

When you multiply `rayDirection` by `totalDistance`, you are scaling that direction. 

If `totalDistance` is `5.3`, the  $vec3(x, y, z)$ triples or quadruples in length until it points to a position exactly `5.3` units away from an imaginary $(0,0,0)$ starting point.

#### The Origin

```glsl
vec3 rayOrigin = vec3(0.0, 0.0, -5.0);
vec3 rayDirection = normalize(vec3(st.x, st.y, -1.0));
float totalDistance = 0.0;
```

If the camera (`rayOrigin`) was sitting exactly at the center of the universe $(0,0,0)$, the scaled direction vector would be the final coordinate (`rayDirection` * `totalDistance`). You wouldn't need to add `rayOrigin` to this.

However, the camera (`rayOrigin`) is usually positioned somewhere else in the 3D world—for example, shifted back along the Z-axis at $(0.0, 0.0, -5.0)$ so you can look at the object.

By adding `rayOrigin`, you take the camera's current coordinate, its origin in 3D space, and offset it by the scaled distance along the ray's path.

**This gives you the current position of the ray at this point.**

--- 

### The Loop

```glsl
 for (int i = 0; i < 64; i++) {
    vec3 currentPos = rayOrigin + rayDirection * totalDistance;
    float safeStep = sdBox(currentPos, box_size);

    if (safeStep < 0.001) {
      hit = 1.0;
      hitPos = currentPos;
      break;
    }

    if (totalDistance > 15.0) {
      break;
    }

    totalDistance += safeStep;
  }

```

The loop repeats this exact calculation up to 64 times.

- **Iteration 0:** 
	- `totalDistance` is initialized to `0.0`.
	$$\text{currentPos} = \text{rayOrigin} + \text{rayDirection} \times 0.0$$
    
1. The calculation evaluates exactly to your camera's location (`rayOrigin`). 
    
```glsl 
float safeStep = sdBox(currentPos, box_size);
```
2. You query [[Signed Distance Fields#3D#Cubes|sdBox]] at the camera's position.
    
- **Iteration 1:** `
	- sdBox` reports that the nearest surface is `2.5` units away. You set `totalDistance = 2.5`. The loop restarts, and the equation recalculates:
    
    $$\text{currentPos} = \text{rayOrigin} + \text{rayDirection} \times 2.5$$
    
    `currentPos` jumps `2.5` units deep into the scene along the camera's sightline.
    
- **Iteration 2:** 
	- You query `sdBox` at this new coordinate. It reports the box is still `0.8` units away. `totalDistance` becomes `3.3`.
    
    $$\text{currentPos} = \text{rayOrigin} + \text{rayDirection} \times 3.3$$
    

The line of code runs completely from scratch on every single iteration of the loop, tracking the front edge of your sampling sphere as it marches deeper into your scene.

#### [[Normals|Surface Normals]]

With the loop successfully calculating where the ray intersects the box, the next step is determining the **[[Normals|Surface Normals]]** at that intersection point (`hitPos`).

```glsl
vec3 hitPos = vec3(0.0);
```

Without a surface normal, you cannot calculate how light [[Reflection (Physics)|Reflects]] off the object. The box will render as a flat, two-dimensional silhouette because every hit pixel will have the exact same flat color value.

In traditional 3D graphics, normals are baked into the 3D model data by an artist. In raymarching, because the scene exists only as mathematical equations, you must calculate the normal using a calculus concept called the **gradient**.

### Gradients

A [[Normals|Surface Normal]]  is a [[Normalization#Normalizing in 3D Space|Normalized Vec3]] (`vec3`) that points directly perpendicular (90 degrees) away from the surface at a specific coordinate.

To find this direction mathematically, you need to look at how the distance values returned by your [[Signed Distance Fields#Signed Distance Functions#3D]] (`sdBox`) change when you shift slightly away from the `hitPos`.

Imagine standing on the side of a hill in complete darkness. If you take a tiny step to the North, a tiny step to the East, and a tiny step Up, you can feel the elevation change under your feet. By comparing those changes, you can deduce exactly which way the hill slopes and which way is straight up. That is what we do to the SDF.

### The Finite Difference Method

To estimate this slope on a GPU, you use the **Finite Difference Method**. 

You sample your SDF six times—slightly offset along the positive and negative sides of the X, Y, and Z axes—using a tiny value called epsilon ($\epsilon$, usually `0.001`).

Here is the complete GLSL function to calculate the normal vector:
Also see [[Swizzling]]

```glsl
vec3 getNormal(vec3 p) {
    // A tiny offset value (epsilon)
    float eps = 0.001;
    
    // An array-like mapping to easily construct offset vectors
    vec2 h = vec2(eps, 0.0);
    
    // Estimate the slope for each axis independently
    float gradX = sdBox(p + h.xyy, vec3(0.8)) - sdBox(p - h.xyy, vec3(0.8));
    float gradY = sdBox(p + h.yxy, vec3(0.8)) - sdBox(p - h.yxy, vec3(0.8));
    float gradZ = sdBox(p + h.yyx, vec3(0.8)) - sdBox(p - h.yyx, vec3(0.8));
    
    // Combine the gradients into a vector and normalize it
    return normalize(vec3(gradX, gradY, gradZ));
}
```

### Step-by-Step Mechanical Breakdown

#### 1. The Vector [[Swizzling]] (`h.xyy`)

To test the X-axis change, you need a vector that represents `(0.001, 0.0, 0.0)`. Instead of creating three separate `vec3` variables for each axis, we use a trick with a `vec2`:

```glsl
vec2 h = vec2(0.001, 0.0);
```

By rearranging the components (called [[swizzling]]), you generate your 3D offset vectors instantly:

- `h.xyy` becomes `vec3(0.001, 0.0, 0.0)`
    
- `h.yxy` becomes `vec3(0.0, 0.001, 0.0)`
    
- `h.yyx` becomes `vec3(0.0, 0.0, 0.001)`
    

#### 2. Calculating Axis Slope (`gradX`)

Look closely at the calculation for the X-axis:

```glsl
float gradX = sdBox(p + h.xyy, vec3(0.8)) - sdBox(p - h.xyy, vec3(0.8));
```

- `sdBox(p + h.xyy, ...)` samples the distance field a tiny bit to the **right**.
    
- `sdBox(p - h.xyy, ...)` samples the distance field a tiny bit to the **left**.
    

By subtracting the left sample from the right sample, you find the difference in distance.

- If the value is **positive**, the distance field is getting larger as you move right; the surface slopes away from you to the left.
    
- If the value is **negative**, the distance field is getting smaller; the surface slopes away to the right.
    
- If the value is **zero**, the field isn't changing along that axis at all.

The code repeats this for `gradY` (up/down) and `gradZ` (forward/backward).
#### 3. Vector Combination and Normalization

```glsl
return normalize(vec3(gradX, gradY, gradZ));
```


Once you bundle these three independent slope values into a `vec3(gradX, gradY, gradZ)`, you have a vector pointing exactly away from the box's surface. 

Finally, you pass it through `normalize()` to scale its geometric length to exactly `1.0`, making it a valid [[Magnitude#3. Unit Vectors $ mathbf{ hat{v}}$|Unit Vector]].

### How to Integrate It Next

In your main function, right inside your `if (safeStep < 0.001)` block where you confirm a hit, you will call this function:

```glsl
if (safeStep < 0.001) {
    hit = 1.0;
    hitPos = currentPos;
    
    // Calculate the surface normal at the exact point of impact
    vec3 normal = getNormal(hitPos);
    
    break;
}
```

Once you have that `normal` vector, you can:
1. Take a constant `vec3 lightDir = normalize(vec3(1.0, 1.0, -1.0))` 
2. Use a dot product to calculate standard diffuse lighting. 

### Coloring The Sides 

```glsl
// --- RENDER ---
  vec3 bgColor = vec3(0.01, 0.01, 0.01);
  vec3 finalColor = bgColor;

  if (hit > 0.5) {
    vec3 normal = getNormal(hitPos, box_size);
    vec3 cubeColor = vec3(1.0); // Fallback color
    // Isolate each face using the direction of the normal vector
    if (normal.x > 0.5) {
      cubeColor = vec3(0.9, 0.2, 0.2); // Right face: Red
    } else if (normal.x < -0.5) {
      cubeColor = vec3(0.2, 0.9, 0.2); // Left face: Green
    } else if (normal.y > 0.5) {
      cubeColor = vec3(0.2, 0.2, 0.9); // Top face: Blue
    } else if (normal.y < -0.5) {
      cubeColor = vec3(0.9, 0.9, 0.2); // Bottom face: Yellow
    } else if (normal.z > 0.5) {
      cubeColor = vec3(0.9, 0.2, 0.9); // Front face: Magenta
    } else if (normal.z < -0.5) {
      cubeColor = vec3(0.2, 0.9, 0.9); // Back face: Cyan
    }

    finalColor = cubeColor;
  }

```

# Next Steps 

### The Problem with Flat Color

Right now, your cube will render as a 2.5D solid-shaded graphic, much like a retro 90s CAD program or an early flat-shaded console game. The colors are vivid, but there is no sense of depth across a single face because the faces themselves are entirely uniform.

To step into realistic 3D space, you need **[[Lambertian Diffuse Shading]]**. 

Instead of hardcoding a color based on the face direction, you scale the brightness of the surface based on how directly it faces an imaginary light source.

### The Next Mechanical Step: Dot Product Lighting

To add lighting, you need to calculate the angle between the surface normal vector and a vector pointing toward your light source. This is achieved instantly on the GPU using the **dot product** instruction (`dot()`).

Mathematically, the dot product of two normalized vectors outputs a single floating-point scalar value:

- **`1.0`** if the surface faces the light perfectly head-on (maximum brightness).
    
- **`0.0`** if the surface is parallel to the light ray (grazing light).
    
- **Negative values** if the surface faces completely away from the light (total shadow).

#### How to implement it in your code:

You can clean out the massive `if/else` block and replace it with direct mathematical scaling.

```glsl
if (hit > 0.5) {
    vec3 normal = getNormal(hitPos, box_size);
    
    // 1. Define a base material color for the entire cube
    vec3 baseColor = vec3(0.8, 0.5, 0.3); // A warm clay color
    
    // 2. Define where the light is coming from (and normalize it)
    vec3 lightPos = vec3(2.0, 4.0, -3.0);
    vec3 lightDir = normalize(lightPos - hitPos);
    
    // 3. Calculate the diffuse lighting intensity using the dot product
    // clamp() or max() prevents negative light values from flipping colors
    float diffuse = max(dot(normal, lightDir), 0.0);
    
    // 4. Add a touch of ambient light so shadows aren't completely pitch black
    float ambient = 0.1;
    float lightIntensity = diffuse + ambient;
    
    // 5. Multiply the base color by the calculated intensity
    finalColor = baseColor * lightIntensity;
}
```

By switching from conditional branching (`if/else`) to vector arithmetic (`dot`), your shader transforms from a flat schematic renderer into an engine capable of calculating realistic continuous shading across smooth or sharp surfaces alike.

![[Pasted image 20260526132605.png|275]]