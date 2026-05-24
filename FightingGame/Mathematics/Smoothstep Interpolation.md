#shaders #math

> https://en.wikipedia.org/wiki/Smoothstep

`smoothstep(edge0, edge1, x)` is a GLSL function that thresholds values, returning `0.0` or `1.0` while smoothly interpolating the boundary. 

It is the standard mechanism in #computer_graphics & #shaders for rendering crisp, anti-aliased geometry instead of hard, pixelated edges.

```glsl
// Draws a smooth circle by interpolating between 0.4 and 0.41
float mask = smoothstep(0.4, 0.41, length(uv)); 
```

### Mathematics

![[Pasted image 20260524071806.png]]