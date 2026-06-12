#shaders #computer_graphics #computer_science 

![[Pasted image 20260524143045.png|345]]

```glsl
#ifdef GL_ES
precision mediump float;
#endif

uniform vec2 u_resolution;

void main() {
  vec2 uv = gl_FragCoord.xy / u_resolution.xy;

  // Fix aspect ratio to ensure the grid squares do not stretch
  uv.x *= u_resolution.x / u_resolution.y;

  // 1. Scale the space to determine the number of grid tiles
  uv *= 25.0;

  // 2. Tile the space.
  // fract() returns only the decimal portion (e.g., 1.2 becomes 0.2).
  // This loops the coordinates from 0.0 to 1.0 repeatedly.
  vec2 gridSpace = fract(uv);

  // 3. Define the line thickness
  float thickness = 0.05;

  // 4. Draw the lines
  // step(edge, x) returns 0.0 if x < edge, and 1.0 if x > edge.
  // By subtracting this from 1.0, we invert it: it returns 1.0 (white)
  // only when the coordinate is extremely close to the tile border.
  float lineX = 1.0 - step(thickness, gridSpace.x);
  float lineY = 1.0 - step(thickness, gridSpace.y);

  // 5. Combine the X and Y lines.
  // max() ensures that if either a vertical OR horizontal line is present,
  // the pixel becomes white.
  float grid = max(lineX, lineY);

  gl_FragColor = vec4(vec3(grid), 1.0);
}

```