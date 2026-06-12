#math #shaders #vector 
# Normalization

**Normalization** is the mathematical process of taking any non-zero vector and scaling it so that its [[Magnitude]] becomes exactly `1`, while completely preserving its original direction. The resulting vector is called a **[[Magnitude#3. Unit Vectors $ mathbf{ hat{v}}$|Unit Vector]]**.

## The Core Concept
The magnitude (length) of a vector applies universally regardless of the number of dimensions. To normalize a vector $\mathbf{v}$, you simply divide the vector by its own [[Magnitude]] $\|\mathbf{v}\|$:

$$ \mathbf{\hat{v}} = \frac{\mathbf{v}}{\|\mathbf{v}\|} $$

Because the Pythagorean theorem (which calculates [[Magnitude]]) scales cleanly into higher dimensions, this exact same division operation normalizes vectors in 2D, 3D, and even N-dimensional space.

### Normalizing in 2D Space
If $\mathbf{v} = (x, y)$:
1. Find the [[Magnitude]]: $\|\mathbf{v}\| = \sqrt{x^2 + y^2}$
2. Divide the vector components: $\mathbf{\hat{v}} = \left( \frac{x}{\|\mathbf{v}\|}, \frac{y}{\|\mathbf{v}\|} \right)$

### Normalizing in 3D Space
If $\mathbf{v} = (x, y, z)$:
1. Find the magnitude: $\|\mathbf{v}\| = \sqrt{x^2 + y^2 + z^2}$
2. Divide the vector components: $\mathbf{\hat{v}} = \left( \frac{x}{\|\mathbf{v}\|}, \frac{y}{\|\mathbf{v}\|}, \frac{z}{\|\mathbf{v}\|} \right)$

### Normalizing in N-Dimensional Space
For any dimension $N$:
$$ \mathbf{\hat{v}} = \frac{1}{\sqrt{\sum_{i=1}^{n} v_i^2}} \begin{bmatrix} v_1 \\ v_2 \\ \vdots \\ v_n \end{bmatrix} $$

> **Note:** You cannot normalize a zero vector $\mathbf{0} = (0, 0)$ because its magnitude is `0`, and division by zero is mathematically undefined.

# Formulas 

$\overset{̂}{\mathbf{u}} = \frac{\mathbf{u}}{\parallel \mathbf{u} \parallel} = \left(\right. \frac{u_{1}}{\parallel \mathbf{u} \parallel} , \frac{u_{2}}{\parallel \mathbf{u} \parallel} , \ldots , \frac{u_{n}}{\parallel \mathbf{u} \parallel} \left.\right)$

> The **normalized vector û** of a non-zero vector **u** is the unit vector in the direction of **u**, i.e. 
> 

## In Game Development & Graphics

Normalization is a ubiquitous operation in 3D graphics, physics engines, and [[GLSL Shaders]].

*   **Direction Vectors:** Normalized vectors are perfect for representing pure direction (e.g., "Where is the camera pointing?", "Which way is the wind blowing?") because they strip away distance information.
*   **Lighting & Shading:** In shaders, surface normals and light directions MUST be normalized to calculate the [[Dot Product]] correctly for Lambertian or Phong lighting models. If they aren't unit length, the lighting equations will output arbitrarily bright or dark artifacts.

### GLSL Implementation
In GLSL, you rarely write the math manually. You use the built-in `normalize` function, which automatically handles the dimension (vec2, vec3, vec4) behind the scenes:

```glsl
vec3 lightDirection = vec3(1.0, 5.0, -2.0);
vec3 unitLightDir = normalize(lightDirection); 
// Now length is exactly 1.0
```
