#math #vector 

If a matrix has only one row or only one column, it is called a **vector**.

A vector represents both a **direction** and a **[[Magnitude]]** (length).

* A matrix having only one row is called a **row vector**.
  $$V_{row} = \begin{bmatrix} 1 & 2 & 3 \end{bmatrix}$$
* A matrix having only one column is called a **column vector**.
  $$V_{col} = \begin{bmatrix} 1 \\ 2 \\ 3 \end{bmatrix}$$

---
  
# Directions

To find the direction of a vector, you use standard trigonometry. 
The tangent of the direction is equal to the opposite side (Y) divided by the adjacent side (X).

$$\tan(\theta) = \frac{Y}{X}$$
$$\theta = \arctan\left(\frac{10}{25}\right) \approx 21.8^\circ$$

The direction of a 2D vector $\vec{v} = \langle x, y \rangle$ is found using the formula $\theta = \tan^{-1}\left(\frac{y}{x}\right)$, where $\theta$ represents the angle the vector makes with the positive x-axis. [1, 2]

## 1. Identify the vector components

Locate the horizontal component $x$ and the vertical component $y$ from your given vector $\vec{v} = \langle x, y \rangle$. [3, 4, 5, 6]

## 2. Calculate the reference angle

Plug the absolute values of $x$ and $y$ into the inverse tangent function to find the reference angle $\theta_{\text{ref}}$:  
$$\theta_{\text{ref}} = \tan^{-1}\left(\left\vert{}\frac{y}{x}\right\vert{}\right)$$

## 3. Adjust for the correct quadrant

Because $\tan^{-1}$ only returns values between $-90^\circ$ and $90^\circ$, you must look at the signs of your original $x$ and $y$ components to determine the true direction angle $\theta$: [7, 8, 9]

- Quadrant I ($+x, +y$): $\theta = \theta_{\text{ref}}$
- Quadrant II ($-x, +y$): $\theta = 180^\circ - \theta_{\text{ref}}$
- Quadrant III ($-x, -y$): $\theta = 180^\circ + \theta_{\text{ref}}$
- Quadrant IV ($+x, -y$): $\theta = 360^\circ - \theta_{\text{ref}}$ [10]

## 4. 3D Vector Directions

For a 3D vector $\vec{v} = \langle x, y, z \rangle$, direction is expressed using direction cosines rather than a single angle. Calculate the vector's magnitude $\vert{}\vec{v}\vert{} = \sqrt{x^2 + y^2 + z^2}$, then find the angles ($\alpha, \beta, \gamma$) relative to the x, y, and z axes:  
$$\cos(\alpha) = \frac{x}{\vert{}\vec{v}\vert{}}, \quad \cos(\beta) = \frac{y}{\vert{}\vec{v}\vert{}}, \quad \cos(\gamma) = \frac{z}{\vert{}\vec{v}\vert{}}$$

---

# [[Rotation Matrix|Rotating Vectors]]
