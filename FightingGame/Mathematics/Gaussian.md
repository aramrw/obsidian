#math #statistics #graphics #linear_algebra

The term **Gaussian** refers to concepts named after **Carl Friedrich Gauss**, one of the most influential mathematicians in history. 

---

## 1. Gaussian Distribution (The "Normal" Distribution)
In [[Statistics and Probability]], the Gaussian distribution is the famous **Bell Curve**. It describes how data clusters around a central mean.

### The Equation (1D):
$$f(x) = \frac{1}{\sigma\sqrt{2\pi}} e^{-\frac{1}{2}\left(\frac{x-\mu}{\sigma}\right)^2}$$
- $\mu$ (mu): The mean (the center of the peak).
- $\sigma$ (sigma): The standard deviation (how "wide" the curve is).

**Why it matters:** Most natural phenomena (heights, test scores, error rates) follow this pattern.

---

## 2. Gaussian Blur (Computer Graphics)
A Gaussian Blur is a common image-processing effect that uses the Gaussian function as a [[Convolution]] kernel to calculate the weight of each pixel for smoothing.

- **How it works:** Instead of a simple average, pixels closer to the center have a higher weight than pixels further away.
- **In Shaders:** You use a "Gaussian Kernel" (a matrix of weights) to sample neighboring pixels in a [[GLSL Shaders|shader]].

---

## 3. Gaussian Elimination (Linear Algebra)
This is the standard algorithm for solving systems of linear equations. It uses "row operations" to transform a matrix into **Row Echelon Form**.

- **The Goal:** To get a [[Matrices|matrix]] into a state where you have 1s on the diagonal and 0s below them, making it easy to find the variables.
- **Connection:** This is a core part of [[Numerical Linear Algebra]].

---

## 4. Gaussian Noise
This is random noise where the intensity of the noise follows a Gaussian distribution.
- **Usage:** Used in [[Perlin Noise]] research and for simulating film grain or sensor static in graphics.

---

## Related Concepts
* [[Statistics and Probability]]
* [[Matrices]]
* [[Numerical Linear Algebra]]
* [[GLSL Shaders]]
