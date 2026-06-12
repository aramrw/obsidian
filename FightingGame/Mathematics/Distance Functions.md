#math #shaders #graphics #geometry

In computer graphics, how you measure distance determines how shapes are rendered. A common mistake in shaders is confusing **Vertical Distance** with **[[Euclidean]] Distance**.

---

## 1. The Math: Vertical vs. Perpendicular

### Vertical Distance ($d_v$)
This is the absolute difference between the pixel's $y$ coordinate and the function's value $f(x)$.
$$d_v = |y - f(x)|$$

This distance only measures along the Y-axis.

In the notation $d_v$, the $v$ simply stands for vertical.

  It is used to distinguish it from other types of distance, like:
   * $d_v$: Vertical distance (measuring only on the Y-axis).
   * $d_e$: Euclidean distance (measuring the shortest straight-line path).
   * $d_x$: Horizontal distance (measuring only on the X-axis).

  In mathematical notation, subscripts like these are used to "label" a variable so
  you know exactly which version of the value you are talking about.

### Euclidean (Perpendicular) Distance ($d_e$)
The true distance is the **shortest path** from a point $P$ to a curve $C$. This is always perpendicular to the curve's tangent.
$$d_e = \min_{P_c \in C} \|P - P_c\|$$

### Why the "Thinning" Happens
On a flat horizontal line, $d_v$ and $d_e$ are identical. However, on a steep slope, the vertical distance to the curve is much larger than the perpendicular distance. 

If you use a fixed threshold (e.g., `step(0.01, d_v)`) to draw a line:
*   **On Peaks/Valleys:** The slope is 0. The line looks its "true" thickness.
*   **On Slopes:** The vertical gap is "stretched." To get to the same vertical distance, you need to be closer to the curve horizontally. This makes the line appear visually **thinner**.

---

## 2. The CS: Shader Implementation

### The "Vertical" Approach (Thin on Slopes)
This is what you found in your shader. It's fast but visually inconsistent.

```glsl
float wave = sin(uv.x * 10.0);
float d_v = abs(uv.y - wave);

// The line thickness is 0.01 vertically, 
// which is less than 0.01 perpendicular on slopes.
float line = 1.0 - step(0.01, d_v);
```

### The "Derivative" Correction
To fix this, we can normalize the distance using the **gradient** (derivative) of the function. This is a common trick in Signed Distance Field (SDF) rendering.

If $f'(x)$ is the slope, the corrected distance is approximately:
$$d \approx \frac{|y - f(x)|}{\sqrt{1 + (f'(x))^2}}$$

```glsl
// y = sin(x) -> dy/dx = cos(x)
float wave = sin(uv.x * 10.0);
float slope = cos(uv.x * 10.0) * 10.0; // Chain rule

float d_v = abs(uv.y - wave);
float corrected_d = d_v / sqrt(1.0 + slope * slope);

float uniform_line = 1.0 - step(0.01, corrected_d);
```

---

## 3. Practical Usage: [[Signed Distance Fields]]
In modern graphics, we prefer using **Signed Distance Functions (SDFs)**. An SDF for a line or curve returns the true Euclidean distance, ensuring that shadows, glows, and outlines remain perfectly uniform regardless of the shape's orientation.

---

## Related Concepts
* [[Euclidean]] (Distance between points)
* [[Vector Calculus]] (Gradients and Derivatives)
* [[Collision Detection]] (Using SDFs for hitboxes)
* [[GLSL Shaders]]
