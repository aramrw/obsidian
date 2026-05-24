#shaders #math #trigonometry #computer_graphics 

In [[GLSL Shaders]] (fragment), the fractional function isolates the decimal part of a number, resulting in a repeating pattern.

---
## Sawtooth

In GLSL, `fract(x)` creates an infinite repeating sawtooth wave from `0.0` to `1.0`. 

![[Pasted image 20260524063956.png|349]]

> Duplicates geometric data across the screen without requiring iterations or loops which makes it good for gpus.

### Core Behavior & Structural Properties

- **Domain & Range:** The function accepts any real number and restricts the output strictly to the range of `[0.0, 1.0)`.
    
- **Discontinuity:** At every whole integer (e.g., **-1, 1, 2, 3**), the value instantly drops from just under **1.0** back down to **0.0**.
    
- **Periodicity:** The wave repeats exactly every **1.0** unit along the axis.

### Common Visual Layout Examples
When applied to graphics and texture coordinates, `fract(x)` is the foundation for repeating patterns, grids, and uv-mapping loops. Here is how it translates visually across different math platforms:

```glsl
// Duplicates the UV coordinate space 'scale' times
vec2 repeatedUV = fract(uv * scale);
```

![[output2 1.gif]]

#### Mathematical Breakdown: Scale = 10.0
To understand how the repeating visual space is generated, here is the exact math the GPU evaluates as it moves across the screen's X-axis using `fract(10.0 * uv.x)`:

| Screen Position (`uv.x`) | Multiplier Math (`10.0 * uv.x`) | `fract()` Output | Visual Result |
| :--- | :--- | :--- | :--- |
| **0.0** (Left edge) | 10.0 * 0.0 = 0.0 | `0.0` | Start of Band 1 |
| **0.05** | 10.0 * 0.05 = 0.5 | `0.5` | Middle of Band 1 |
| **0.099** | 10.0 * 0.099 = 0.99 | `0.99` | End of Band 1 (Bright) |
| **0.1** | 10.0 * 0.1 = 1.0 | **`0.0`** | **Reset!** (Start of Band 2) |
| **0.15** | 10.0 * 0.15 = 1.5 | `0.5` | Middle of Band 2 |
| **0.2** | 10.0 * 0.2 = 2.0 | **`0.0`** | **Reset!** (Start of Band 3) |
| ... | ... | ... | ... |
| **0.9** | 10.0 * 0.9 = 9.0 | **`0.0`** | **Reset!** (Start of Band 10) |
| **1.0** (Right edge) | 10.0 * 1.0 = 10.0 | **`0.0`** | **Final Reset** |

Because the screen stops at `1.0`, the inner math peaks exactly at `10.0`. The function is forced to cross 10 whole integers, resulting in 10 resets and 10 repeating bands.

***

![[output2 1.gif]]

--- 

# Related

- [[GLSL Shaders#Coordinate Space Mathematics]]