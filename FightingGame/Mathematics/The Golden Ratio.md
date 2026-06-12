https://en.wikipedia.org/wiki/Golden_ratio

> ($\phi \approx 1.618$)

### The Golden Reciprocal $1/\phi$

The golden ratio ($\phi \approx 1.618$) and its reciprocal ($1/\phi \approx 0.618$) are famous for being the "most irrational" numbers. Because $1/\phi$ cannot be approximated well by any simple fraction, it is incredibly useful for avoiding predictable, repeating patterns.

- **Golden-Section Search:** When building custom engines or writing shaders, calculating derivatives to find the minimum or maximum of a complex curve is computationally expensive. Golden-section search is an algorithm that finds the extreme points of a function purely through iterative narrowing. By shrinking the search area by a ratio of $1/\phi$ each iteration, the algorithm reuses previous calculations perfectly. It is structurally the most efficient way for a CPU to hone in on a value without using calculus.
    
- **Procedural Geometry & Distribution:** If you are procedurally spawning objects in 2D or 3D space (like particle systems, bullet-hell projectiles, or organic terrain), you want them densely packed without overlapping in ugly, repeating straight lines. If you rotate your spawn point by a standard fraction (like $1/4$ or $1/3$ of a circle), the objects will stack up perfectly and leave empty gaps. By rotating exactly $1/\phi$ of a turn (the Golden Angle) for each new object, the maximum irrationality guarantees the pattern will _never_ perfectly align with itself, resulting in a mathematically perfect, organic distribution.

## The Golden Rectangle & Shader Example

A **Golden Rectangle** is one where the aspect ratio is exactly $\phi : 1$ (or $1 : \phi$).

Its most fascinating geometric property is self-similarity: if you cut a perfect square out of a Golden Rectangle, the remaining area is a smaller rectangle that shares the exact same aspect ratio. You can repeat this process infinitely.

If you connect the opposite corners of these diminishing squares with quarter-circle arcs, it perfectly forms the **Golden Spiral**.

We have a dedicated [[GLSL Shaders|shader]] demonstrating this visual subdivision process.
* **Location:** `/Programming/glsl_shaders/golden_ratio/golden_ratio.frag`
* It procedurally draws the bounding box, iteratively splits the largest dimension into a square, and draws the bounding golden spiral arc, fading in each recursive step over time.