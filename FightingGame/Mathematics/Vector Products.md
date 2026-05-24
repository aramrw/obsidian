#math #vectors #shaders

Vector products allow us to calculate relationships between two vectors, such as the angle between them or the direction they both face away from.

---

## 1. Dot Product ($\cdot$)

The **dot product** takes two vectors and returns a **scalar** (a single number). It is also known as the *scalar product*.

### Geometric Formula
$$\mathbf{a} \cdot \mathbf{b} = \|\mathbf{a}\| \|\mathbf{b}\| \cos \theta$$
*   If $\mathbf{a} \cdot \mathbf{b} > 0$: The vectors point in the same general direction (angle < 90°).
*   If $\mathbf{a} \cdot \mathbf{b} = 0$: The vectors are **orthogonal** (perpendicular, 90°).
*   If $\mathbf{a} \cdot \mathbf{b} < 0$: The vectors point in opposite directions (angle > 90°).

### Algebraic Formula (for 2D/3D)
$$\mathbf{a} \cdot \mathbf{b} = a_x b_x + a_y b_y + a_z b_z$$

```glsl
// 1. A typical mobile screen in portrait mode
float screen_width = 1080.0;
float screen_height = 1920.0;

// 2. Calculate the Aspect Ratio
// 1080.0 / 1920.0 = 0.5625
float aspect_ratio = screen_width / screen_height;
```

### The 1.0 Rule

Because you are dividing width by height, `1.0` is your perfect square.

- **Result > 1.0**: The screen is wider than it is tall (Landscape).
    
- **Result < 1.0**: The screen is taller than it is wide (Portrait).
    
- **Result == 1.0**: The screen is a perfect square.

### Practical Applications
*   **Lighting (Lambertian):** Calculating how much light hits a surface by taking the dot product of the surface normal and the light direction.
*   **Visibility/Field of View:** Checking if an enemy is in front of or behind the player.
*   **Projection:** Finding the component of one vector that lies along another.

---

## 2. Cross Product ($\times$)

The **cross product** takes two 3D vectors and returns a **new 3D vector** that is perpendicular to both.

### Geometric Formula
$$\|\mathbf{a} \times \mathbf{b}\| = \|\mathbf{a}\| \|\mathbf{b}\| \sin \theta$$
The direction of the result is determined by the **Right-Hand Rule**.

### Algebraic Formula
$$\mathbf{a} \times \mathbf{b} = \begin{bmatrix} a_y b_z - a_z b_y \\ a_z b_x - a_x b_z \\ a_x b_y - a_y b_x \end{bmatrix}$$

### Practical Applications
*   **Surface Normals:** Calculating the "up" direction of a triangle (plane) by crossing two of its edges.
*   **Torque:** Calculating rotational force in physics engines.
- **Orthonormal Basis:** Generating a full 3D coordinate system ($X, Y, Z$) from just two vectors.

---

## 3. Code Examples

### GLSL: Visualizing the Dot Product (Diffuse Lighting)
In a fragment shader, the dot product is the standard way to calculate how "bright" a pixel is based on a light source.

```glsl
#version 120

uniform float u_time;
uniform vec2 u_resolution;

void main() {
    // 1. Normalize UV coordinates from 0.0 -> 1.0
    vec2 uv = gl_FragCoord.xy / u_resolution;
    
    // 2. Center the UVs so 0,0 is the middle of the screen (-1.0 to 1.0)
    // This makes math like sin/cos for circular motion align with the screen center.
    uv = uv * 2.0 - 1.0;
    
    // Fix aspect ratio so our light moves in a perfect circle, not an oval
    uv.x *= u_resolution.x / u_resolution.y;

    vec3 normal = vec3(0.0, 0.0, 1.0); // Surface still faces straight out

    // 3. Define the light's actual position in 3D space
    // X and Y orbit in a circle. Z is the height of the light hovering above the screen.
    vec3 lightPos = vec3(sin(u_time), cos(u_time), 0.5);

    // 4. Calculate direction FROM the current pixel (uv) TO the light
    // We give the pixel a Z of 0.0 since it lays flat on the screen
    vec3 pixelPos = vec3(uv, 0.0);
    vec3 lightDir = normalize(lightPos - pixelPos);

    // 5. Calculate the diffuse lighting
    float diffuse = max(dot(normal, lightDir), 0.0);

    // Add a little drop-off (attenuation) so the light fades as it gets further away
    float distance = length(lightPos - pixelPos);
    diffuse *= 1.0 / (1.0 + distance * distance);

    gl_FragColor = vec4(vec3(diffuse), 1.0);
}

```

### GLSL: Visualizing the Cross Product (Generating Normals)
You can use the cross product to find the "slope" direction of a 2D heightmap (like a sine wave) to create fake 3D lighting.

```glsl
void main() {
    vec2 uv = gl_FragCoord.xy / u_resolution;
    float eps = 0.01;

    // Sample height at current pixel and two neighbors
    float h = sin(uv.x * 10.0);
    float h_x = sin((uv.x + eps) * 10.0);
    float h_y = h; // height doesn't change on Y in this example

    // Create two vectors along the surface
    vec3 va = normalize(vec3(eps, 0.0, h_x - h));
    vec3 vb = normalize(vec3(0.0, eps, h_y - h));

    // The cross product gives us the vector sticking "out" of the surface
    vec3 normal = cross(va, vb);

    gl_FragColor = vec4(normal * 0.5 + 0.5, 1.0); // Visualize normal as color
}
```

### Rust
```rust
impl Vector3 {
    pub fn dot(&self, other: &Self) -> f64 {
        self.x * other.x + self.y * other.y + self.z * other.z
    }

    pub fn cross(&self, other: &Self) -> Self {
        Self {
            x: self.y * other.z - self.z * other.y,
            y: self.z * other.x - self.x * other.z,
            z: self.x * other.y - self.y * other.x,
        }
    }
}
```

---

## Related Concepts
* [[Vectors]]
* [[GLSL Shaders]]
* [[Euclidean]] (Distance)
* [[Quaternions]] (Rotation)
