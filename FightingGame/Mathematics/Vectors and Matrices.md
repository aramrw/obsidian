#math #matrix #vector

**Source:** [Marco Taboga, PhD - StatLect](https://www.statlect.com/matrix-algebra/vectors-and-matrices)

This lecture provides an informal introduction to [[Matrices|matrices]] and [[Vectors|vectors]].

---

## 1. Matrix
A **matrix** is a two-dimensional array that has a fixed number of rows and columns and contains a number at the intersection of each row and column. 

A matrix is usually delimited by square brackets.

### Example
Here is an example of a $2 \times 2$ matrix:
$$A = \begin{bmatrix} a & b \\ c & d \end{bmatrix}$$

---

## 2. Dimension of a Matrix
If a matrix has $K$ rows and $L$ columns, we say that it has **dimension** $K \times L$, or that it is a $K \times L$ matrix.

### Example
A matrix with $2$ rows and $3$ columns is a $2 \times 3$ matrix:
$$A = \begin{bmatrix} 1 & 2 & 3 \\ 4 & 5 & 6 \end{bmatrix}$$

---

## 3. Entries of a Matrix
The numbers contained in a matrix are called **entries** of the matrix (or elements, or components).

If $A$ is a matrix, the entry at the intersection of row $k$ and column $l$ is usually denoted by $A_{k,l}$ or $A_{kl}$. We say that it is the $(k,l)$-th entry of $A$.

### Example
Let $A$ be a $3 \times 2$ matrix. The element at the third row and first column is denoted as $A_{3,1}$.

---
### 4. [[Vectors]]
---

## 5. Scalars
A matrix having only one row and one column ($1 \times 1$) is called a **scalar**. In other words, a scalar is a single real number.

---

## 6. Equal Matrices
Two $K \times L$ matrices $A$ and $B$ having the same dimension are said to be **equal** if and only if all their corresponding elements are equal to each other:
$$A_{k,l} = B_{k,l} \quad \forall \ k, l$$
### Examples

```rust
/// A 2D Matrix with K rows and L columns
#[derive(Debug, Clone, Copy, PartialEq)]
pub struct Matrix<const K: usize, const L: usize> {
    pub data: [[f64; K]; L], 
}

impl<const K: usize, const L: usize> Matrix<K, L> {
    /// Creates a new matrix from raw 2D array data
    pub fn new(data: [[f64; K]; L]) -> Self {
        Self { data }
    }
}
```

```rust
fn main() {
    // A 2x3 Matrix (2 rows, 3 columns)
    let matrix_a = Matrix::new([
        [1.0, 2.0, 3.0],
        [4.0, 5.0, 6.0],
    ]);

    // A Row Vector is just a 1xK Matrix
    let row_vector = Matrix::new([
        [1.0, 2.0, 3.0]
    ]);

    // A Column Vector is just an Lx1 Matrix
    let col_vector = Matrix::new([
        [1.0],
        [2.0],
        [3.0]
    ]);

    println!("Matrix A: {:?}", matrix_a);
}
```

---

## 7. Zero Matrices
A matrix $A$ is a **zero matrix** if all its elements are equal to zero, denoted as:
$$A = 0$$

### Example
A $2 \times 2$ zero matrix looks like:
$$0_{2\times2} = \begin{bmatrix} 0 & 0 \\ 0 & 0 \end{bmatrix}$$

---

## 8. Square Matrices
A $K \times L$ matrix is called a **square matrix** if the number of its rows is exactly equal to the number of its columns ($K = L$).
$$A_{3\times3} = \begin{bmatrix} 1 & 2 & 3 \\ 4 & 5 & 6 \\ 7 & 8 & 9 \end{bmatrix}$$

---

## 9. Diagonal and Off-Diagonal Elements
Let $A$ be a square matrix.
* The **diagonal** (or main diagonal) of $A$ is the set of all entries $A_{k,l}$ such that $k = l$.
* Elements belonging to this line are called **diagonal elements**.
* All other entries are called **off-diagonal elements**.

### Example
In a $3 \times 3$ matrix, the entries $A_{1,1}$, $A_{2,2}$, and $A_{3,3}$ make up the main diagonal:
$$A_{3\times3} = \begin{bmatrix} (1) & 2 & 3 \\ 4 & (5) & 6 \\ 7 & 8 & (9) \end{bmatrix}$$

---

## 10. Identity Matrix
A square matrix is called an **identity matrix** if all its diagonal elements are equal to $1$ and all its off-diagonal elements are equal to $0$. It is universally indicated by the letter $I$.

### Example
The $3 \times 3$ identity matrix:
$$I = \begin{bmatrix} 1 & 0 & 0 \\ 0 & 1 & 0 \\ 0 & 0 & 1 \end{bmatrix}$$

---

## 11. Transpose of a Matrix
If $A$ is a $K \times L$ matrix, its **transpose** (denoted by $A^{\top}$ or $A^T$) is the $L \times K$ matrix where the rows and columns are swapped. 

Mathematically, the $(l,k)$-th element of $A^{\top}$ is equal to the $(k,l)$-th element of $A$:
$$(A^{\top})_{l,k} = A_{k,l}$$

* The columns of $A^{\top}$ are equal to the rows of $A$.
* The rows of $A^{\top}$ are equal to the columns of $A$.

---

## 12. Transpose Properties & Related Concepts
* [[Matrix Multiplication]]
* [[Matrix Addition]]
* [[Determinant]]
* [[Inverse Matrix]]
* [[Vector Spaces]]
* [[Eigenvalues and Eigenvectors]]
* [[Graph Theory]]
* [[Statistics and Probability]]

---

## 13. Symmetric Matrices
A square matrix is said to be **symmetric** if it is exactly equal to its transpose:
$$A = A^{\top}$$

---

## Solved Exercises

### Exercise 1
Let $A$ be a $3 \times 3$ matrix:
$$A = \begin{bmatrix} 1 & 2 & 3 \\ 4 & 5 & 6 \\ 7 & 8 & 9 \end{bmatrix}$$
Find its transpose $A^{\top}$.

**Solution:**
$$A^{\top} = \begin{bmatrix} 1 & 4 & 7 \\ 2 & 5 & 8 \\ 3 & 6 & 9 \end{bmatrix}$$

### Exercise 2
Let $A$ be a $3 \times 1$ column vector:
$$A = \begin{bmatrix} 1 \\ 2 \\ 3 \end{bmatrix}$$
Show that its transpose is a row vector.

**Solution:**
Since $A$ has 3 rows and 1 column, swapping them gives a matrix with 1 row and 3 columns (a row vector):
$$A^{\top} = \begin{bmatrix} 1 & 2 & 3 \end{bmatrix}$$

### Exercise 3
Is the following matrix symmetric?
$$A = \begin{bmatrix} 1 & 2 & 3 \\ 0 & 5 & 6 \\ 0 & 0 & 9 \end{bmatrix}$$

**Solution:**
No. Finding its transpose yields:
$$A^{\top} = \begin{bmatrix} 1 & 0 & 0 \\ 2 & 5 & 0 \\ 3 & 6 & 9 \end{bmatrix}$$
Since $A \neq A^{\top}$, it is **not** symmetric.