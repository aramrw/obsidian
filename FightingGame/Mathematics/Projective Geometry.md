#math #geometry #graphics #linear_algebra

# Projective Geometry

Projective Geometry is the study of geometric properties that are invariant under projection. In computer graphics, this is the fundamental math used to map a 3D world onto a 2D screen.

---

## 1. The Core Concept: Perspective
In standard Euclidean geometry, parallel lines never meet. In **Projective Geometry**, parallel lines meet at a **"Point at Infinity"** (think of railroad tracks appearing to touch on the horizon).

---

## 2. Homogeneous Coordinates ($w$)
To perform projections and translations using [[Matrices]], we add an extra dimension called $w$.

A 3D point $(x, y, z)$ becomes a 4D homogeneous coordinate:
$$(x, y, z, w)$$

### Why $w$ matters:
1. **Translation:** You cannot represent "moving" a point using a $3 \times 3$ matrix. By adding $w$ and using a $4 \times 4$ matrix, translation becomes possible.
2. **Perspective Division:** After multiplying by a projection matrix, we divide $x, y, z$ by $w$. 
   - If $w$ is large, the object is far away and becomes smaller.
   - If $w$ is small, the object is close and appears larger.

---

## 3. The Pinhole Camera Model
This is the mathematical model of how a camera (or eye) works. It maps a 3D point $\mathbf{P}$ to a 2D point $\mathbf{p}$ on the "image plane" using similar triangles.

$$\frac{x}{z} = \frac{x'}{f}$$
Where $f$ is the focal length.

---

## 4. Homographies
A **Homography** is a transformation (a $3 \times 3$ matrix) that maps one plane to another.
* **Usage:** Used in "AR" to pin a virtual image onto a flat surface (like a table) or for "stitching" photos together to create a panorama.

---

## 5. Duality
One of the most beautiful parts of Projective Geometry. In 2D projective space:
- Every two **points** define a **line**.
- Every two **lines** define a **point**.
They are "dual" to each other—whatever is true for points is also true for lines.

---

## Related Concepts
* [[Matrices]] (specifically $4 \times 4$ Projection Matrices)
* [[Vectors]]
* [[GLSL Shaders]] (where `gl_Position` is always a `vec4` because of $w$)
* [[Simple Raytracing]]
