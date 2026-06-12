#math 

https://en.wikipedia.org/wiki/Nabla_symbol

> The **nabla** is a triangular symbol resembling an inverted Greek [delta](https://en.wikipedia.org/wiki/Delta_\(letter\) "Delta (letter)"):∇ or ∇. 
> The name comes, by reason of the symbol's shape, from the [Hellenistic Greek](https://en.wikipedia.org/wiki/Hellenistic_Greek "Hellenistic Greek") word νάβλα for a [Phoenician harp](https://en.wikipedia.org/wiki/Nabla_\(instrument\) "Nabla (instrument)")

In mathematics, $\nabla f$ ==represents the gradient of a scalar function== $f$. The symbol $\nabla$ itself is called nabla (or del), and it acts as a vector [[Differential]] operator. [1, 2, 3, 4]

## 1. Mathematical Definition

When you apply the nabla operator to a multivariable scalar function $f(x, y, z)$, it packages all of the first-order partial derivatives of that function into a single vector: [5, 6]

$$\nabla f = \left( \frac{\partial f}{\partial x}, \frac{\partial f}{\partial y}, \frac{\partial f}{\partial z} \right)$$

For a function of $n$ variables, $f(x_1, x_2, \dots, x_n)$, it expands analogously into an $n$-dimensional vector field: [4]

$$\nabla f = \left( \frac{\partial f}{\partial x_1}, \frac{\partial f}{\partial x_2}, \dots, \frac{\partial f}{\partial x_n} \right)$$

## 2. Physical Meaning

The gradient vector gives you two crucial pieces of information about the function at any given point: [1, 7]

- Direction: It points exactly in the direction of the steepest ascent (where the function increases most rapidly).
- Magnitude: The length of the vector ($\vert{}\nabla f\vert{}$) represents the maximum rate of change (slope) in that steepest direction. [1, 5]

## 3. Quick Example

If you have the 2D function $f(x, y) = 3x^2 + 5y$, its partial derivatives are:

- $\frac{\partial f}{\partial x} = 6x$
- $\frac{\partial f}{\partial y} = 5$

Therefore, the gradient is the vector function:

$$\nabla f = (6x, 5)$$

Evaluating this at a specific point like $(1, 2)$ results in $\nabla f(1, 2) = (6, 5)$. This means that from the point $(1, 2)$, moving along the vector direction $(6, 5)$ will yield the fastest possible increase in the value of $f$. [5, 8]

## 4. Other Uses of Nabla ($\nabla$)

While $\nabla f$ stands for the gradient, the nabla symbol is also used as a shorthand tool for other core multivariable operations when combined with vectors: [9, 10]

- Divergence ($\nabla \cdot \mathbf{F}$): The dot product with a vector field, measuring the net outward flow from a point.
- Curl ($\nabla \times \mathbf{F}$): The cross product with a vector field, measuring the rotation or spin at a point.
- Laplacian ($\nabla^2 f$ or $\Delta f$): The divergence of the gradient, measuring the average value deviation of a function around a point. [9, 11, 12, 13, 14]
