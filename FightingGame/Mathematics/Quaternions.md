#math #geometry #rotation #complex_numbers

# Quaternions

Quaternions are a number system that extends [[Complex Numbers]]. While [[Complex Numbers]] have one imaginary unit ($i$), quaternions have three ($i, j, k$). They are the industry standard for representing 3D rotations in computer graphics and aerospace.

---

## 1. The Definition
A quaternion $q$ is represented as:
$$q = a + bi + cj + dk$$
Where $a, b, c, d$ are real numbers and $i, j, k$ are imaginary units.

### Hamilton's Rule
The fundamental identity discovered by William Rowan Hamilton:
$$i^2 = j^2 = k^2 = ijk = -1$$

This leads to the non-commutative multiplication rules:
- $ij = k, \quad ji = -k$
- $jk = i, \quad kj = -i$
- $ki = j, \quad ik = -j$

---

## 2. Rotations: Quaternions vs. Matrices
In 3D graphics, we use **Unit Quaternions** (where $\|q\| = 1$) to represent rotations.

| Feature | Euler Angles | Matrices ($3 \times 3$) | Quaternions |
| :--- | :--- | :--- | :--- |
| **Storage** | 3 numbers | 9 numbers | 4 numbers |
| **Interpolation** | Jerky/Broken | Hard to calculate | Smooth (SLERP) |
| **Gimbal Lock** | Yes (Major issue) | No | No |
| **Efficiency** | High | Low | High |

---

## 3. SLERP (Spherical Linear Interpolation)
One of the biggest advantages of quaternions is **SLERP**. It allows you to smoothly animate between two rotation states (like a character's arm moving) along the shortest path on a sphere.

---

## 4. Usage in Shaders
While many shaders use [[Matrices]] for projection, quaternions are often used in the CPU-side physics engine or for skeletal animation before being passed to the GPU.

---

## Related Concepts
* [[Vectors]]
* [[Matrices]]
* [[GLSL Shaders]]
* [[Simple Raytracing]]
