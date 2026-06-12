#math #vector #trigonometry #geometry #shaders #linear_algebra 

> In [linear algebra](https://en.wikipedia.org/wiki/Linear_algebra "Linear algebra"), a **rotation matrix** is a [transformation matrix](https://en.wikipedia.org/wiki/Transformation_matrix "Transformation matrix") that is used to perform a [rotation](https://en.wikipedia.org/wiki/Rotation_\(mathematics\) "Rotation (mathematics)") in [Euclidean space](https://en.wikipedia.org/wiki/Euclidean_space "Euclidean space"). For example, using the convention below, the [[Matrix]]

> [Wikipedia](https://en.wikipedia.org/wiki/Rotation_matrix)
> [KhanAcademy/LinearTransformations](https://www.khanacademy.org/v/linear-transformation-examples-rotations-in-r2)

The mathematical operation `rayOrigin.yz = rotate2D(rayOrigin.yz, 0.5)` rotates a 2D point (or a pair of coordinates) counterclockwise by an angle of $0.5$ radians around the origin.

Here is a practice math problem to calculate exactly how this transformation alters a specific set of coordinates.

---

## 3D [[Vectors|Vector]] Rotation

Given a 3D point $\mathbf{P} = (x, y, z) = (2.0, 1.0, 0.0)$, find the new coordinates of $\mathbf{P}$ after applying the transformation:  
$$\mathbf{P.yz} = \text{rotate2D}(\mathbf{P.yz}, 0.5)$$

_Note: Assume the rotation angle $0.5$ is in radians._

---

## 1. Isolate the Coordinates to Rotate

The code strictly modifies the `.yz` components of the vector. The $x$-coordinate remains completely unchanged. [1]

- $x_{\text{new}} = 2.0$
- Initial 2D vector to rotate: $\begin{pmatrix} y \\ z \end{pmatrix} = \begin{pmatrix} 1.0 \\ 0.0 \end{pmatrix}$

## 2. Set Up the 2D Rotation Matrix

 > **The Cheat Sheet:** To change directions or axes, look at the negative sign.
 - Negative in **top-right**: Counter-Clockwise.
- Negative in **bottom-left**: Clockwise.

A standard 2D counterclockwise rotation matrix for an angle $\theta$ is defined as:  
$$R(\theta) = \begin{pmatrix} \cos\theta & -\sin\theta \\ \sin\theta & \cos\theta \end{pmatrix}$$

For $\theta = 0.5$ radians: 
$$R(0.5) = \begin{pmatrix} \cos(0.5) & -\sin(0.5) \\ \sin(0.5) & \cos(0.5) \end{pmatrix}$$

- $\cos(0.5) \approx 0.8776$
- $\sin(0.5) \approx 0.4794$

Substituting these into the matrix yields:  
$$R(0.5) = \begin{pmatrix} 0.8776 & -0.4794 \\ 0.4794 & 0.8776 \end{pmatrix}$$

## 3. Multiply the Matrix by the Vector 

Initial 2D vector to rotate: $\begin{pmatrix} y \\ z \end{pmatrix} = \begin{pmatrix} 1.0 \\ 0.0 \end{pmatrix}$

Multiply the rotation matrix by the intiial 2d vector:  
$$\begin{pmatrix} y_{\text{new}} \\ z_{\text{new}} \end{pmatrix} = \begin{pmatrix} 0.8776 & -0.4794 \\ 0.4794 & 0.8776 \end{pmatrix} \begin{pmatrix} 1.0 \\ 0.0 \end{pmatrix}$$

$$\begin{pmatrix} y_{\text{new}} \\ z_{\text{new}} \end{pmatrix} = \begin{pmatrix} (0.8776 \times 1.0) + (-0.4794 \times 0.0) \\ (0.4794 \times 1.0) + (0.8776 \times 0.0) \end{pmatrix} = \begin{pmatrix} 0.8776 \\ 0.4794 \end{pmatrix}$$

## 4. Reconstruct the Final 3D Vector

Combine the unaltered $x$-coordinate with the newly calculated $y$ and $z$ coordinates.

The final transformed 3D point is approximately $(2.0, 0.8776, 0.4794)$.

