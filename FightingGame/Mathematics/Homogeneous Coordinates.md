#math #graphics #linear_algebra

In standard [[Euclidean]] geometry, a point in 3D space is represented as $(x, y, z)$. In computer graphics, we add a fourth component, **$w$**, to create **Homogeneous Coordinates**: $(x, y, z, w)$.

---

## 1. Why do we need $w$?

### A. Translation with Matrices
Standard $3 \times 3$ [[Matrices]] can only represent **Linear Transformations** (rotation, scaling, shearing). Mathematically, these always keep the origin $(0,0,0)$ at $(0,0,0)$. Translation moves the origin, which is why it is an **Affine Transformation**.

In 3D, translation is an *addition*:
$$\mathbf{v}' = \mathbf{v} + \mathbf{t}$$

But matrix math is *multiplication*:
$$\mathbf{v}' = M \mathbf{v}$$

To perform an addition using only multiplication, we use a "trick" by adding a 4th dimension. A translation in 3D is mathematically identical to a **shear** in 4D.

#### The Translation Matrix Breakdown
When we multiply a point $(x, y, z, 1)$ by a translation matrix $T$:

$$\begin{bmatrix} 1 & 0 & 0 & t_x \\ 0 & 1 & 0 & t_y \\ 0 & 0 & 1 & t_z \\ 0 & 0 & 0 & 1 \end{bmatrix} \begin{bmatrix} x \\ y \\ z \\ 1 \end{bmatrix} = \begin{bmatrix} (1 \cdot x) + (0 \cdot y) + (0 \cdot z) + (t_x \cdot 1) \\ (0 \cdot x) + (1 \cdot y) + (0 \cdot z) + (t_y \cdot 1) \\ (0 \cdot x) + (0 \cdot y) + (1 \cdot z) + (t_z \cdot 1) \\ (0 \cdot x) + (0 \cdot y) + (0 \cdot z) + (1 \cdot 1) \end{bmatrix} = \begin{bmatrix} x + t_x \\ y + t_y \\ z + t_z \\ 1 \end{bmatrix}$$

Because $w = 1$, the translation values $t_x, t_y, t_z$ are "activated" and added to the coordinates.

### B. Perspective Projection
In a 3D game, objects that are far away should look smaller. 
- The $w$ component acts as a "scaling factor." 
- The final 3D position on your screen is calculated by **Perspective Division**:
  $$\text{Final } X = x / w, \quad \text{Final } Y = y / w$$
- This is why parallel lines appear to meet at the horizon—as $z$ (depth) increases, $w$ increases, making the $X$ and $Y$ coordinates shrink toward the center.

---

## 2. Points vs. Vectors
Homogeneous coordinates allow us to distinguish between a **point** (a location in space) and a **vector** (a direction).

- **Point:** Set $w = 1$. It can be translated.
- **Vector:** Set $w = 0$. It cannot be moved (because a direction doesn't have a "position"), but it can still be rotated and scaled.

---

## 3. In GLSL Shaders
Every vertex shader output (`gl_Position`) is a `vec4`. 
- The GPU takes your `vec4(x, y, z, w)`, performs the division by $w$ automatically, and maps the result to the screen pixels.

---

## Related Concepts
* [[Projective Geometry]]
* [[Matrices]]
* [[GLSL Shaders]]
* [[Vectors]]
