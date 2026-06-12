#math #geometry #trigonometry #shaders

## Sphere Normal Maps

In #computer_graphics , a normal [[Vectors|Vector]] describes the direction a surface is facing. For a **unit sphere** centered at the origin, any point on its surface $(x, y, z)$ is exactly equal to its normal vector at that point. 

We can generate a procedural 2D normal map of a sphere perfectly by using math instead of textures.

```glsl
// Author:
// Title:

#ifdef GL_ES
precision mediump float;
#endif

uniform vec2 u_resolution;
uniform vec2 u_mouse;
uniform float u_time;

vec3 sphereNormals(in vec2 uv) {
    // 1. Tile the space 
    // remap UVs to [-1.0, 1.0] with (0,0) at the center
    uv = fract(uv) * 2.0 - 1.0; 
    
    vec3 ret;
    ret.xy = uv; // Note: sqrt(uv*uv)*sign(uv) is mathematically identical to uv
    
    // 2. Derive Z using the Sphere Equation
    ret.z = sqrt(abs(1.0 - dot(ret.xy, ret.xy)));
    
    // 3. Remap from Normal space [-1.0, 1.0] to Color space [0.0, 1.0]
    ret = ret * 0.5 + 0.5;    
    
    // 4. Mask out the corners to create a circle
    return mix(vec3(0.0), ret, smoothstep(1.0, 0.98, dot(uv, uv)));
}

void main() {
    vec2 st = gl_FragCoord.xy/u_resolution.xy;
    st.x *= u_resolution.x/u_resolution.y;

    vec3 color = vec3(0.);
    color = vec3(st.x,st.y,abs(sin(u_time)));
    vec3 sphere = sphereNormals(st);

    gl_FragColor = vec4(sphere,1.0);
}
}
```

### The Math: Deriving Z

How do we get a 3D sphere from a flat 2D `uv` plane? We use the equation of a unit sphere:

$$x^2 + y^2 + z^2 = 1$$

Since we already know $x$ and $y$ (they are our `uv` coordinates mapped from `-1` to `1`), we just need to isolate $z$ (the depth / height of the sphere pointing towards the camera):

$$z^2 = 1 - (x^2 + y^2)$$
$$z = \sqrt{1 - (x^2 + y^2)}$$

In GLSL, $x^2 + y^2$ is equivalent to the dot product of the 2D vector with itself (`dot(uv, uv)`).

### Why Normal Maps are Blue/Purple
Before rendering, we must remap the vectors. Normal vectors range from `-1.0` to `1.0`, but color channels range from `0.0` to `1.0`. 
By doing `ret * 0.5 + 0.5`, we shift the values:
- A vector pointing straight toward the camera is $(0, 0, 1)$.
- Remapped, it becomes $(0.5, 0.5, 1.0)$.
- In RGB space, Red=0.5, Green=0.5, Blue=1.0 is the exact signature purplish-blue color you see on flat surfaces in standard normal maps!

---

# [[Distance Functions]]

---
### Related Concepts
- [[Space Repetition]] (The `fract()` call)
- [[Interpolation]] (The `mix()` and `smoothstep()` calls)
- [[Vectors Products]] (The `dot()` product)