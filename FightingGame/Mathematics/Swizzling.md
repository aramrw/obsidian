#computer_graphics #math #vectors 

https://en.wikipedia.org/wiki/Swizzling_(computer_graphics)

> In [computer graphics](https://en.wikipedia.org/wiki/Computer_graphics "Computer graphics"), **swizzles** are a class of operations that transform [[Vectors]] by rearranging components (in any way you want).

If you have a 2D vector variable named `position` where `x = 5` and `y = 10`:

- **`xy`**: Accesses the components in their original order.
- **`yx`**: Flips the components (creates a new vector where the new X is 10, and the new Y is 5).
- **`xyy`**: Converts a 2D vector into a 3D vector by duplicating the Y component.
- **`yxy`**: Creates a 3D vector using the Y, X, and Y values in that exact sequence.

```glsl
vec2 point = vec2(1.0, 2.0); // A 2D vector: x=1.0, y=2.0

vec2 flipped = point.yx;     // Returns vec2(2.0, 1.0)
vec3 3d_point = point.xyy;   // Returns vec3(1.0, 2.0, 2.0)
vec4 4d_point = point.yxyx;  // Returns vec4(2.0, 1.0, 2.0, 1.0)

```

# Examples

> Excerpt from [[Cube Shader]] & [[RayMarching#The Finite Difference Method]]

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

`eps` (epsilon) is your tiny test step—your "foot" stepping out. It’s only `0.001` units wide because you want to sample the space immediately right next to your hit point `p`.

By putting it in a `vec2` where `h.x = 0.001` and `h.y = 0.0`, we can easily create 3D offset directions using **swizzling**:

- `h.xyy` becomes `vec3(0.001, 0.0, 0.0)` — A step to the **Right**.
    
- `h.yxy` becomes `vec3(0.0, 0.001, 0.0)` — A step **Up**.
    
- `h.yyx` becomes `vec3(0.0, 0.0, 0.001)` — A step **Forward**.

