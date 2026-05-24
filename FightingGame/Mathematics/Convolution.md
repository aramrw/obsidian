#math #dsp #signals #shaders

Convolution is a mathematical operation on two functions that produces a third function expressing how the shape of one is modified by the other. It is the core of digital filtering, reverb, and image processing.

---

## 1. The Definition

In discrete systems (like digital audio), convolution is the sum of the products of two sequences as one "slides" over the other.

$$(f * g)[n] = \sum_{m=-\infty}^{\infty} f[m] \cdot g[n-m]$$

*   **$f$**: The input signal (the audio).
*   **$g$**: The **kernel** or **Impulse Response (IR)**.

---

## 2. Impulse Response (IR)

An Impulse Response is a mathematical snapshot of how a system reacts to a single, infinitely sharp spike of sound (a "Dirac Delta" pulse).

*   **Reverb:** To simulate a cathedral, you record an IR of a starter pistol firing in that cathedral. By convolving your dry audio with that IR, your audio "takes on" the acoustics of the space.
*   **EQ/Filtering:** Low-pass and high-pass filters are implemented by convolving audio with specific kernels that suppress certain frequencies.

---

## 3. 2D Convolution (Image Processing)

In shaders and image processing, convolution is used for bluring, sharpening, and edge detection. The "kernel" is a small matrix (e.g., $3 \times 3$) that slides over the pixels.

### Example: Gaussian Blur
The kernel is a $[[Gaussian]]$ distribution.

$$\text{Kernel} = \frac{1}{16} \begin{bmatrix} 1 & 2 & 1 \\ 2 & 4 & 2 \\ 1 & 2 & 1 \end{bmatrix}$$

Applying this kernel to every pixel results in a blurred image.

---

## 4. Properties

*   **Commutative:** $f * g = g * f$
*   **Associative:** $f * (g * h) = (f * g) * h$
*   **Convolution Theorem:** Convolution in the time domain is equivalent to **point-wise multiplication** in the frequency domain ($[[Complex Numbers]]$ and FFTs). This makes complex filtering significantly faster.

---

## Related Concepts
* [[Audio Processing]]
* [[Gaussian]] (Blurring)
* [[Matrices]] (2D kernels)
* [[Complex Numbers]] (FFT-based convolution)
