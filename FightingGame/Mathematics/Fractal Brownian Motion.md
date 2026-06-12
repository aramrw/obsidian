https://en.wikipedia.org/wiki/Fractional_Brownian_motion

 > fBm is a [continuous-time](https://en.wikipedia.org/wiki/Continuous-time_stochastic_process "Continuous-time stochastic process") [Gaussian process](https://en.wikipedia.org/wiki/Gaussian_process "Gaussian process") BH(t)![{\textstyle B_{H}(t)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/56f38f90d783ea72693e35eede38cd59ee1a04e3) on [0,T]![{\textstyle [0,T]}](https://wikimedia.org/api/rest_v1/media/math/render/svg/ac1e853156820c6967c42328401568e1a0736da2), that starts at zero, has [expectation](https://en.wikipedia.org/wiki/Expectation_\(mathematics\) "Expectation (mathematics)") zero for all t![{\displaystyle t}](https://wikimedia.org/api/rest_v1/media/math/render/svg/65658b7b223af9e1acc877d848888ecdb4466560) in [0,T]![{\textstyle [0,T]}](https://wikimedia.org/api/rest_v1/media/math/render/svg/ac1e853156820c6967c42328401568e1a0736da2), and has the following [covariance function](https://en.wikipedia.org/wiki/Covariance_function "Covariance function"):

${\displaystyle E[B_{H}(t)B_{H}(s)]={\tfrac {1}{2}}(|t|^{2H}+|s|^{2H}-|t-s|^{2H}),}$

> where _H_ is a real number in (0, 1), called the [Hurst index](https://en.wikipedia.org/wiki/Hurst_exponent "Hurst exponent") or Hurst parameter associated with the fractional Brownian motion. The Hurst exponent describes the raggedness of the resultant motion, with a higher value leading to a smoother motion. It was introduced by [Mandelbrot & van Ness (1968)](https://en.wikipedia.org/wiki/Fractional_Brownian_motion#CITEREFMandelbrotvan_Ness1968).

--- 

## Computer Graphics

 Used to construct complex, detailed textures by overlaying multiple layers of noise, known as **octaves**. 
 
 Each subsequent layer features a higher frequency (smaller, denser structures) and a lower amplitude (reduced visual weight).

### 1. Mathematical Concept: The FBM Equation

Mathematically, a 4-octave FBM accumulates noise values using a geometric progression for both amplitude and frequency:

$$f(p) = \sum_{i=0}^{3} A_i \cdot \text{noise}(p_i)$$

Where $A_i$ represents the amplitude of octave $i$, and $p_i$ represents the transformed spatial coordinate for that octave.

### 2. Step-by-Step Code vs. Math Breakdown

#### Layer 1: The Base Octave

The process begins by initializing the [[Accumulator]] and sampling the first layer of noise.

- **Math:** The noise function outputs values from $0.0$ to $1.0$. To create symmetric variance, the value must be converted to signed noise ranging from $-1.0$ to $1.0$:
    
    $$\text{Signed Noise} = 2.0 \cdot \text{noise}(p) - 1.0$$
    
    This is scaled by the initial base amplitude ($A_0 = 0.5$).
    
- **Code:**
    
    OpenGL Shading Language
    
    ```
    float f = 0.0;
    f += 0.5000 * (-1.0 + 2.0 * noise(p));
    ```
    

### Coordinate Transformation (Lacunarity and Rotation)

Before computing the next layer, the coordinates must be modified so the patterns do not perfectly align and create artificial repetition.

- **Math:** The coordinate space is scaled by a factor roughly equal to $2.0$ (lacunarity) and rotated using a pre-defined transformation matrix to break axial symmetry:
    
    $$p_{next} = \mathbf{M} \cdot p \cdot 2.02$$
    
- **Code:**
    ```glsl
    p = mtx * p * 2.02;
    ```
    

### Layers 2, 3, and 4: Accumulating Detail

The sequence repeats. Each layer halves the amplitude ($0.25$, $0.125$, $0.0625$) and roughly doubles the spatial frequency ($2.03$, $2.01$).

- **Math:**
    
    The subsequent terms add progressively finer details:
    
    $$f \leftarrow f + 0.2500 \cdot \text{Signed Noise}(p_1)$$
    
    $$f \leftarrow f + 0.1250 \cdot \text{Signed Noise}(p_2)$$
    
    $$f \leftarrow f + 0.0625 \cdot \text{Signed Noise}(p_3)$$
    
- **Code:**
    ```glsl
    f += 0.2500 * (-1.0 + 2.0 * noise(p)); p = mtx * p * 2.03;
    f += 0.1250 * (-1.0 + 2.0 * noise(p)); p = mtx * p * 2.01;
    f += 0.0625 * (-1.0 + 2.0 * noise(p));
    ```
    

### Normalization

Because multiple values are added together, the total accumulated value can exceed the normalized range of $[-1.0, 1.0]$.

- **Math:**
    
    The maximum possible value of $f$ occurs if every single noise sample yields its maximum output ($1.0$). This maximum is the sum of all amplitudes used:
    
    $$\text{Max Total Amplitude} = 0.5 + 0.25 + 0.125 + 0.0625 = 0.9375$$
    
    Dividing the accumulated total by this sum scales the final value back precisely into the bounded range of $[-1.0, 1.0]$.
    
- **Code:**
    ```glsl
    return f / 0.9375;
    ```
    

## The Complete Consolidated Loop

In production code, this linear progression is mathematically equivalent to executing a loop over the number of desired octaves:

|**Operational Parameter**|**Value / Modification**|
|---|---|
|**Octaves**|4|
|**Amplitude Multiplier (Gain)**|$0.5$ per step|
|**Frequency Multiplier (Lacunarity)**|$\approx 2.0$ per step + Rotation|
|**Output Bounds**|Scaling ensures normalized amplitude range|