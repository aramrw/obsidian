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

When applied to graphics and texture coordinates, `fract(x)` is the foundation for repeating patterns, grids, and uv-mapping loops. Here is how it translates visually across different math platforms:

```glsl
// Duplicates the UV coordinate space 'scale' times
vec2 repeatedUV = fract(uv * scale);
```

![[output2 1.gif]]

--- 

# Related

- [[GLSL Shaders#Coordinate Space Mathematics]]