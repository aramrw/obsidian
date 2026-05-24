#math #linear_algebra #matrix

# Eigenvalues and Eigenvectors

Eigenvalues and eigenvectors are fundamental concepts in linear algebra that describe how a linear transformation (represented by a [[Vectors and Matrices#8. Square Matrices]]) scales space in certain directions.

---

## 1. The Core Idea
When a matrix $A$ multiplies a vector $v$, the vector usually changes both its **[[Magnitude]]** and its **direction**.

However, for a specific matrix $A$, there are special vectors $v$ that **do not change direction** when multiplied by $A$. They only get scaled by a constant factor $\lambda$.

The equation is:
$$Av = \lambda v$$

- $v$ is the **eigenvector**.
- $\lambda$ (lambda) is the **eigenvalue**.

---

## 2. The Characteristic Equation
To find the eigenvalues, we rewrite the equation as:
$$(A - \lambda I)v = 0$$
For a non-zero vector $v$ to exist, the matrix $(A - \lambda I)$ must be singular (its determinant must be zero). This gives us the **characteristic equation**:
$$\det(A - \lambda I) = 0$$

### Example ($2 \times 2$)
Let $A = \begin{bmatrix} 4 & 1 \\ 2 & 3 \end{bmatrix}$.
1. Subtract $\lambda$ from the diagonal: $A - \lambda I = \begin{bmatrix} 4-\lambda & 1 \\ 2 & 3-\lambda \end{bmatrix}$.
2. Calculate the determinant: $(4-\lambda)(3-\lambda) - (1)(2) = 0$.
3. Solve the quadratic: $\lambda^2 - 7\lambda + 10 = 0 \implies (\lambda-5)(\lambda-2) = 0$.
4. The eigenvalues are $\lambda_1 = 5$ and $\lambda_2 = 2$.

---

## 3. Eigenspace
The set of all eigenvectors associated with a specific eigenvalue $\lambda$, along with the zero vector, is called the **eigenspace** of $\lambda$. It is a subspace of the vector space.

---

## 4. Why They Matter
- **Stability Analysis:** Used in physics and engineering to see if a system will collapse or remain stable.
- **PCA (Principal Component Analysis):** Used in AI/Data Science to reduce the "noise" in data by finding the directions of maximum variance.
- **PageRank:** Google's original algorithm treats the internet as a giant matrix and finds the "principal eigenvector" to rank pages.
- **Vibration:** Used to find the natural frequencies of buildings and bridges.

---

## Related Concepts
* [[Matrices]]
* [[Determinant]]
* [[Vector Spaces]]
* [[Numerical Linear Algebra]]
* [[Complex Numbers]]
