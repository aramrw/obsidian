#shaders #math
# UV Normalization

UV Normalization establishes `(0,0)` at the center of the viewport and corrects for the aspect ratio of the screen.

When manipulating pixels, the underlying forces dictating the coordinate space must be understood. Normalizing the UV coordinates transforms the screen from a pixel grid into a consistent mathematical plane, making it resolution-independent.

Typically, this looks like:
```glsl
// Corrects aspect ratio and sets (0,0) to center
vec2 uv = (fragCoord - 0.5 * iResolution.xy) / iResolution.y;
```