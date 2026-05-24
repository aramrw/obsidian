#math #matrix #shaders

Affine transformations are geometric transformations that preserve lines and parallelism (but not necessarily distances or angles). In game engines, these are used to move, rotate, and scale everything from characters to UI elements.

---

## 1. The Transformation Matrix

In 3D, we use a $4 \times 4$ matrix and [[Homogeneous Coordinates]] ($vec4$) to represent these transformations in a single pass.

### Translation (Moving)
To move a point by $(t_x, t_y, t_z)$:
$$T = \begin{bmatrix} 1 & 0 & 0 & t_x \\ 0 & 1 & 0 & t_y \\ 0 & 0 & 1 & t_z \\ 0 & 0 & 0 & 1 \end{bmatrix}$$

### Scaling (Resizing)
To scale by factors $(s_x, s_y, s_z)$:
$$S = \begin{bmatrix} s_x & 0 & 0 & 0 \\ 0 & s_y & 0 & 0 \\ 0 & 0 & s_z & 0 \\ 0 & 0 & 0 & 1 \end{bmatrix}$$

---

## 2. Rotation (2D)

To rotate a point by angle $\theta$ around the origin:
$$R = \begin{bmatrix} \cos \theta & -\sin \theta \\ \sin \theta & \cos \theta \end{bmatrix}$$

In shaders, rotations are often done manually using $[[Trigonometry]]$ functions.

---

## 3. Combining Transformations (TRS)

Matrix multiplication is **not commutative** ($A \times B \neq B \times A$). The order in which you apply transformations matters. 

The standard order for game engines is **TRS**:
1.  **T**ranslate
2.  **R**otate
3.  **S**cale

$$\mathbf{v}' = M_{\text{translate}} \times M_{\text{rotate}} \times M_{\text{scale}} \times \mathbf{v}$$

*Note: In code, this often looks reversed depending on whether you use row-major or column-major math.*

---

## 4. Practical Application: Vertex Shaders

The "Model-View-Projection" (MVP) matrix is the most common use of affine transformations in graphics.

```glsl
#version 300 es

layout(location = 0) in vec3 a_position;
uniform mat4 u_model;
uniform mat4 u_view;
uniform mat4 u_projection;

void main() {
    // Applying all transformations to the vertex position
    gl_Position = u_projection * u_view * u_model * vec4(a_position, 1.0);
}
```

---

## Related Concepts
* [[Matrices]]
* [[Homogeneous Coordinates]]
* [[GLSL Shaders]]
* [[Vectors and Matrices]]
* [[Quaternions]] (Better for 3D rotations)
