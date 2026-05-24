#shaders #math #computer_graphics
# Color Generation

In procedural shader programming, colors are rarely static. Instead of loading textures, shaders calculate pixel colors mathematically based on time, space (UV coordinates), and geometric distance. 

This is often done using a combination of dynamic variables, thresholding functions like `step()`, and interpolation functions like `mix()`.

## Procedural Color Example
Let's break down a complex color generation block from the [[Tan-Wave Shader]] tutorial:

```glsl
// Color generation
float p = tan(uv.x + u_time);
vec3 bg_color = vec3(0.1, 0.1, 0.1);
vec3 fg_color = vec3(
    p * 0.1 + step(0.1, abs(cos(clock * 2.0)) * uv.x), 
    p * 0.9, 
    0.1 + step(1.0, sin(clock) * sin(clock) * abs(uv.x))
);

vec3 final_color = mix(bg_color, fg_color, d);

// Alpha modulation based on quantized grid distance
float alpha = d * sin(ttime + 1.0 - floor(length(floor(uuv * 10.0))));

gl_FragColor = vec4(final_color, alpha);
```

### 1. Dynamic Variables (`p`)
```glsl
float p = tan(uv.x + u_time);
```
The variable `p` establishes a base oscillation using the tangent of the current X coordinate and the elapsed time. Because it uses `tan`, `p` will periodically spike to infinity, creating sharp bands of intensity that scroll horizontally over time.

### 2. The Foreground Color (`fg_color`)
Instead of a solid RGB value, `fg_color` calculates each color channel (Red, Green, Blue) independently using spatial and temporal math:

```glsl
vec3 fg_color = vec3(
    p * 0.1 + step(0.1, abs(cos(clock * 2.0)) * uv.x), 
    p * 0.9, 
    0.1 + step(1.0, sin(clock) * sin(clock) * abs(uv.x))
);
```

##### **Red Channel:** 
```glsl
p * 0.1 + step(0.1, abs(cos(clock * 2.0)) * uv.x)
```
  - Adds a fraction of our tangent wave `p`.
  - Uses `step()` to create a hard threshold. It multiplies a cosine time wave by the spatial X coordinate `uv.x`. Whenever this product exceeds `0.1`, it instantly adds a bright red flash.
##### **Green Channel:** 
```glsl
p * 0.9
```
  - Dominated almost entirely by the raw tangent wave, meaning the overall aesthetic will have strong, pulsing green vertical bands.
##### **Blue Channel:**
```glsl
0.1 + step(1.0, sin(clock) * sin(clock) * abs(uv.x))
```
  - Establishes a baseline blue tint (`0.1`).
  - Uses `step()` alongside the square of a sine wave (ensuring it is always positive) to occasionally spike the blue channel to max intensity when the condition is met.

### 3. Interpolation (`mix()`)
```glsl
vec3 final_color = mix(bg_color, fg_color, d);
```
Rather than choosing one color, `mix()` blends the dark `bg_color` and the chaotic, dynamic `fg_color`. The interpolant here is `d`, which usually represents a geometric mask (like a grid or a shape generated from [[Space Repetition]] or [[Smoothstep Interpolation]]). 

Where `d` is `0.0`, the pixel is completely dark gray. Where `d` is `1.0`, the pixel adopts the pulsing procedural foreground color.

### 4. Alpha Quantization (Stepping Artifacts)
```glsl
float alpha = d * sin(ttime + 1.0 - floor(length(floor(uuv * 10.0))));
```
This final step creates deliberate "lo-fi" or blocky artifacts:
1. `floor(uuv * 10.0)` scales the original, undistorted UV coordinates by 10 and floors them, effectively dividing the screen into a chunky 10x10 grid.
2. `length()` calculates the distance from the center of this blocky grid.
3. This blocky distance offsets a sine wave over time (`ttime`), causing the transparency (`alpha`) of the shader to pulse in discrete, chunky blocks rather than a smooth gradient.

---

### Related Concepts
- [[Interpolation]]
- [[Space Repetition]]
- [[Trigonometry]]