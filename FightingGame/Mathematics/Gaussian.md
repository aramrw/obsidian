#math #statistics #graphics #linear_algebra #computer_graphics 

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

## 2.  Computer Graphics
### Gaussian Blur
A Gaussian Blur is a common image-processing effect that uses the Gaussian function as a [[Convolution]] kernel to calculate the weight of each pixel for smoothing.

- **How it works:** Instead of a simple average, pixels closer to the center have a higher weight than pixels further away.
- **In Shaders:** You use a "Gaussian Kernel" (a matrix of weights) to sample neighboring pixels in a [[GLSL Shaders|shader]].

---

### **Gaussian Fog Density**
Commonly used in 3D graphics (like OpenGL or GameEngines) to simulate atmospheric haze.

$$
f(t) = e^{0.004t^2}
$$

```glsl
float fog = exp(-0.04 * t * t);
vec3 planeColor = mix(vec3(0.15), vec3(0.85), pattern);
vec3 horizonColor = vec3(0.4, 0.6, 0.9);
finalColor = mix(horizonColor, planeColor, fog);
```

Where:

- $f(t)$ (or `fog`) is the fog factor. 
	- > `1.0` means no fog (fully visible object).
	 > `0.0` means full fog (completely hidden object).
- $e$ is [[Euler's Number]] ($\approx 2.71828$).  Not to be confused with [[Euler's Constant]].
	- > represented by `exp()` in code.
- $t$ is typically the distance from the camera (or time).
- $0.04$ is the squared density factor $(d^2)$. 
	- > This means the base density coefficient $d$ is $\sqrt{0.04} = 0.2$.

##### 📉 How It Behaves

This specific equation is known as Exponential Squared Fog ($e^{-(d \cdot t)^2}$).
Here is how the fog factor drops off as distance ($t$) increases:

- At $t = 0$ (Close): $f(0) = e^{0} = 1.0 \rightarrow$ Clear visibility.
- At $t = 5$ (Medium): $f(5) = e^{-1} \approx 0.37 \rightarrow$ Heavy fog (37% visibility).
- At $t = 10$ (Far): $f(10) = e^{-4} \approx 0.018 \rightarrow$ Object is almost completely hidden.

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
