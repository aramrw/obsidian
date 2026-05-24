#math #algebra #complex_numbers

# Complex Numbers

A **complex number** is a number that can be expressed in the form $a + bi$, where $a$ and $b$ are real numbers, and $i$ is the **imaginary unit**, which satisfies the equation $i^2 = -1$.

---

## 0. The Origin of $i$
The symbol $i$ for $\sqrt{-1}$ was first introduced by **Leonhard Euler** in 1777. 

Before Euler, the concept of "imaginary" numbers was often dismissed as impossible or useless. **René Descartes** actually coined the term "imaginary" in 1637 as a derogatory name, intending to mock the idea. 

However, it was **Gerolamo Cardano** in the 1500s who first realized that you *had* to use these "impossible" numbers to solve cubic equations, even if the final answer was a real number.

---

## 1. The Anatomy
For a complex number $z = a + bi$:
- $a$ is the **real part**, denoted by $\text{Re}(z)$.
- $b$ is the **imaginary part**, denoted by $\text{Im}(z)$.

---

## 2. The Complex Plane (Argand Diagram)
Complex numbers can be visualized as points or vectors in a 2D plane:
- The **x-axis** represents the real part.
- The **y-axis** represents the imaginary part.

---

## 3. Operations

### Addition
$$(a + bi) + (c + di) = (a + c) + (b + d)i$$

### Multiplication
$$(a + bi)(c + di) = ac + adi + bci + bdi^2 = (ac - bd) + (ad + bc)i$$

### Conjugate
The conjugate of $z = a + bi$ is $\bar{z} = a - bi$. Multiplying a number by its conjugate always results in a real number:
$$z\bar{z} = a^2 + b^2$$

---

## 4. Euler's Formula
One of the most important formulas in mathematics, connecting complex numbers to trigonometry:
$$e^{i\theta} = \cos \theta + i \sin \theta$$

---

## 5. Why They Matter in Programming/Graphics
- **Fractals:** The Mandelbrot set and Julia sets are calculated entirely using complex number iteration.
- **Signal Processing:** Fast Fourier Transforms (FFT) use complex numbers to analyze frequencies (used in audio and image compression).
- **Rotations:** Complex numbers of the form $e^{i\theta}$ can represent 2D rotations, similar to how [[Quaternions]] represent 3D rotations.

---

## Related Concepts
* [[Vectors]]
* [[Quaternions]]
* [[Trigonometry]]
* [[Audio Processing]] (FFTs and Signals)
* [[Eigenvalues and Eigenvectors]] (Complex eigenvalues often represent rotation/oscillation)
