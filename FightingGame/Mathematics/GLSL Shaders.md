#shaders #computer_graphics #math 

# The Syntax 

### Version

> Version of GLSL. Example is 2.0

```js
#version 300 es 
```

### Immutable Variables

> This is an input variable. The `in` keyword means it's read-only data being handed to this shader by the GPU pipeline. The GPU is handing your program a **struct** called `uv` that contains the exact **X & Y coords** of the specific pixel this thread is currently calculating.

```js 
in vec2 uv;
```

### Mutable Variables

> The `out` keyword means this is the **memory block you are responsible for writing the final result into**. In vertex shaders, `gl_Position` is a `vec4` because it uses [[Homogeneous Coordinates]].

```d
out vec4 out_color;
```

### Time 

> `u_time` tracks the elapsed time since the shader started

```glsl
uniform float u_time;
```

### Examples

> Simply converts a pixels position to red and green. For example the first pixel at `(0.0, 0.0)` would become green, since green is `(0.0, 0.0)`.

```js
#version 300 es
precision highp float;

// The vertex shader passes us the normalized coordinates 
// (0.0 to 1.0)
in vec2 uv; 

// We declare a variable to hold our final pixel color
out vec4 out_color;

void main() {
    // Map the X and Y coordinates directly to Red and Green
    out_color = vec4(uv.x, uv.y, 0.0, 1.0);
}
```



The Wave Equation is essential for creating animated procedural effects like water, wind, or pulsing lights. See [[Trigonometry#Traveling Wave Equation]]

$$y = A \sin(kx - \omega t) + D$$

### Coordinate Space Mathematics

Before manipulating pixels, the underlying forces dictating the coordinate space must be understood:

> **Shaders transform the screen from a pixel grid into a mathematical plane**.

- [[UV Normalization]]: Establishes `(0,0)` at the center of the viewport, correcting for aspect ratio.
- [[Space Repetition]]: Uses `fract(x)` to duplicate geometric data across the screen without requiring iterations or loops.
- [[Domain Warping]]: Distorts the coordinate space before drawing shapes. Avoids asymptotes by using continuous functions like [[Simplex Noise]].
- [[Smoothstep Interpolation]]: The standard mechanism for rendering crisp, anti-aliased geometry.

### Important Concepts

- [[Vectors and Matrices]]
- [[Trigonometry]] (The Wave Equation)
- [[Vector Products]] 
	- ([[Dot Product]]/[[Cross Product]])
- [[Interpolation]] 
	- ([[Lerp]]/[[Smoothstep Interpolation]])
- [[Affine Transformations]] 
	- ([[MVP Matrices]])
- [[Planes]]
- [[Rays]] & [[Simple Raytracing]]

### Tutorials 
- [[Tan-Wave Shader]]
- [[Pixel Water Shader]]
- [[Radial Universe Shader]]
- [[Skybox Shader]]