#math #physics #vectors

# Cross Product

The **Cross Product** (denoted by $\times$) is a mathematical operation on two vectors in 3D space that results in a *new, third vector* that is perfectly perpendicular (orthogonal) to both of the original vectors.

Unlike the [[Dot Product]] (which returns a single number/scalar), the cross product returns a vector. 

## The Right-Hand Rule
The direction of the resulting vector is determined by the "right-hand rule". If you point your index finger in the direction of vector $A$, and your middle finger in the direction of vector $B$, your thumb will point in the direction of $A \times B$.

## Formula

Given two 3D vectors $A = (A_x, A_y, A_z)$ and $B = (B_x, B_y, B_z)$, the cross product is calculated as:

$$A \times B = (A_yB_z - A_zB_y, A_zB_x - A_xB_z, A_xB_y - A_yB_x)$$

> **Geometric Meaning of Magnitude:** The [[Magnitude]] (length) of the cross product vector is equal to the area of the [[Parallelogram]] formed by the two original vectors. If the cross product is zero, the vectors are parallel.

## Applications in Game Dev

1. **Calculating [[Normals]]:** If you have three points of a triangle (a polygon on a 3D model), you can create two vectors along its edges. The cross product of those two vectors gives you the "surface normal" (the direction the triangle is facing), which is required for lighting in [[GLSL Shaders]].

![[Pasted image 20260527111415.png|256]]

2. **[[Torque]] and Rotation:** In physics, the cross product is used to calculate [[torque]] (angular force) and angular momentum.
3. **Camera Systems:** Used to calculate the "right" vector of a camera when you have the "forward" direction and the world's "up" direction.

## GLSL Example
GLSL has a built-in function for this.

```glsl
vec3 vectorA = vec3(1.0, 0.0, 0.0); // Pointing Right
vec3 vectorB = vec3(0.0, 1.0, 0.0); // Pointing Up

// Result will be (0.0, 0.0, 1.0) - Pointing Forward towards the camera
vec3 orthogonalVector = cross(vectorA, vectorB);
```
