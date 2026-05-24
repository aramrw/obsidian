#shaders #math
# Smoothstep Interpolation

`smoothstep(edge0, edge1, x)` is a GLSL function that thresholds values, returning `0.0` or `1.0` while smoothly interpolating the boundary. 

It is the standard mechanism in shader programming for rendering crisp, anti-aliased geometry instead of hard, pixelated edges.

```glsl
// Draws a smooth circle by interpolating between 0.4 and 0.41
float mask = smoothstep(0.4, 0.41, length(uv)); 
```