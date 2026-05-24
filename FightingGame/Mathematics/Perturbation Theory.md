#math #floats

[Wikipedia](https://en.wikipedia.org/wiki/Perturbation_theory)

> In [mathematics](https://en.wikipedia.org/wiki/Mathematics "Mathematics") and [applied mathematics](https://en.wikipedia.org/wiki/Applied_mathematics "Applied mathematics"), **perturbation theory** comprises methods for finding an [approximate solution](https://en.wikipedia.org/wiki/Approximation_theory "Approximation theory") to a problem, by starting from the exact [solution](https://en.wikipedia.org/wiki/Solution_\(equation\) "Solution (equation)") of a related, simpler problem.

> Successive terms in the series at higher powers of **ε** usually become smaller. An approximate 'perturbation solution' is obtained by truncating the series, often keeping only the first two terms, the solution to the known problem and the 'first order' perturbation correction.

## Examples

#### Mandlebrot

Instead of calculating the expensive formula for every single pixel on the screen independently, you use a brilliant linear approximation trick:

1. **The Reference Orbit:** You pick _one single pixel_ in the very center of your screen and calculate its incredibly deep orbit using slow, ultra-high arbitrary precision. Let's call this path $X_n$.
    
2. **The Perturbation:** For every other pixel on the screen, you don't calculate its absolute position. Instead, you only calculate its tiny **delta** (the offset vector, $\Delta c$) relative to that center pixel.
    
3. **The Low-Precision Loop:** Through algebraic manipulation, the massive numbers cancel out, leaving a linearized system that tracks how the delta evolves ($\Delta z_n$).
    

Because $\Delta z_n$ is a tiny number, the entire grid's iterations can be calculated using standard, lightning-fast hardware `f32` or `f64` values on your GPU, even if you are zoomed in to a depth of $10^{-1000}$!

#### [[Minimum Bounding Box]]es

To make this render infinitely, you represent your viewport transformations using a formal matrix structure. As you shift and zoom, you maintain a [[minimum bounding box]] transformation matrix.