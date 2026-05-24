#math #calculus #physics

# Vector Calculus

Vector calculus is the study of differentiation and integration of vector fields. It is essential for understanding physics (electromagnetism, fluid dynamics) and advanced computer graphics.

---

## 1. The Gradient ($\nabla f$)
The gradient takes a **scalar field** (like a height map) and produces a **vector field**. It points in the direction of the steepest ascent.

$$\nabla f = \left( \frac{\partial f}{\partial x}, \frac{\partial f}{\partial y}, \frac{\partial f}{\partial z} \right)$$

* **In Graphics:** Used to calculate surface normals from height maps and for "Gradient Descent" in Machine Learning.

---

## 2. Divergence ($\nabla \cdot \mathbf{F}$)
Divergence takes a **vector field** and produces a **scalar**. It measures the "outward flow" of a field from a point.

$$\text{div } \mathbf{F} = \nabla \cdot \mathbf{F} = \frac{\partial F_x}{\partial x} + \frac{\partial F_y}{\partial y} + \frac{\partial F_z}{\partial z}$$

* **Positive Divergence:** A "source" (like a sprinkler).
* **Negative Divergence:** A "sink" (like a drain).
* **In Physics:** Used in [[Diffusion]] and fluid simulations.

---

## 3. Curl ($\nabla \times \mathbf{F}$)
Curl takes a **vector field** and produces another **vector field**. It measures the rotation or "vorticity" of the field at a point.

$$\text{curl } \mathbf{F} = \nabla \times \mathbf{F} = \begin{vmatrix} \mathbf{i} & \mathbf{j} & \mathbf{k} \\ \frac{\partial}{\partial x} & \frac{\partial}{\partial y} & \frac{\partial}{\partial z} \\ F_x & F_y & F_z \end{vmatrix}$$

* **In Physics:** Essential for Maxwell's Equations (Electromagnetism) and simulating whirlpools in water.

---

## 4. The Laplacian ($\nabla^2 f$)
The Laplacian is the divergence of the gradient ($\nabla \cdot \nabla f$). 

$$\nabla^2 f = \frac{\partial^2 f}{\partial x^2} + \frac{\partial^2 f}{\partial y^2} + \frac{\partial^2 f}{\partial z^2}$$

* **Usage:** Used in the heat equation, wave equation, and for smoothing meshes in 3D modeling.

---

## Related Concepts
* [[Vectors]]
* [[Diffusion]]
* [[Perlin Noise]]
* [[GLSL Shaders]]
