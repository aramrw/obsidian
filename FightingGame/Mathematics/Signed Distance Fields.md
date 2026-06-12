https://en.wikipedia.org/wiki/Signed_distance_function

# Signed Distance Functions 

> Functions in space (2D or 3D) that return:
- A negative number if its outside
- 0.0 if its exact on the point
- A positive number if its inside 
## 3D

---

### Cubes 

```glsl
// 1. Signed Distance Field for a 3D Box
float sdBox(vec3 p, vec3 b) {
  vec3 q = abs(p) - b;
  return length(max(q, 0.0)) + min(max(q.x, max(q.y, q.z)), 0.0);
}
```

The function takes a point `p` and the box's half-extents `b` (the distance from the center to each face along the X, Y, and Z axes). 

An example of a perfect cube's half-extents (like in the [[Cube Shader]]) would be $vec3(8.0, 8.0, 8.0)$

- `vec3 q = abs(p) - b;`
    - This mirrors the point into the positive octant, reducing the problem to a single corner.
    - Component values of `q` represent the distance from the point to each face.
- `length(max(q, 0.0))`
    - Calculates the distance to the box when the point is **outside** the box.

#### Formula 

> Expresses the exact distance from an arbitrary 3D point $\mathbf{p} = (x, y, z)$ to the surface of a cube centered at the origin with half-extents $\mathbf{b} = (b_x, b_y, b_z)$.

$$f(\mathbf{p}, \mathbf{b}) = \sqrt{\sum_{i \in \{x,y,z\}} \max(|p_i| - b_i, 0)^2} + \min\left(\max_{i \in \{x,y,z\}} (|p_i| - b_i), 0\right)$$

---

### [[Spheres]]

The Signed Distance Function (SDF) for a sphere centered at the origin with radius $r$ is 

$$f(\mathbf{p}) = \Vert{}\mathbf{p}\Vert{} - r$$

In this formula, $\mathbf{p}$ represents the 3D coordinates of the evaluation point $(x, y, z)$, and $\Vert{}\mathbf{p}\Vert{}$ is the Euclidean distance from the origin, calculated as $\sqrt{x^2 + y^2 + z^2}$.

## Properties of the Sign

The value of the function tells you exactly where the point lies relative to the sphere's surface: [1]

- $f(\mathbf{p}) > 0$: The point is outside the sphere.
- $f(\mathbf{p}) = 0$: The point is exactly on the surface of the sphere.
- $f(\mathbf{p}) < 0$: The point is inside the sphere. [2]

## General Formula (Arbitrary Center)

If your sphere is not at the origin but is centered at a specific position $\mathbf{c} = (c_x, c_y, c_z)$, the formula shifts to account for the offset:

$$f(\mathbf{p}) = \Vert{}\mathbf{p} - \mathbf{c}\Vert{} - r$$

$$f(x, y, z) = \sqrt{(x - c_x)^2 + (y - c_y)^2 + (z - c_z)^2} - r$$

## Code Implementation

Here is how you can implement this efficiently in common programming languages for graphics and shaders:

```glsl
// GLSL (Shader Language)
float sdfSphere(vec3 p, vec3 center, float radius) {
    return length(p - center) - radius;
}
```

```python
# Python
import math

def sdf_sphere(p, center, radius):
    # p and center are tuples or lists of (x, y, z)
    distance = math.sqrt((p[0]-center[0])**2 + (p[1]-center[1])**2 + (p[2]-center[2])**2)
    return distance - radius
```

