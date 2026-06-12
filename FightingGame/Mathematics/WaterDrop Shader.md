#shaders #computer_graphics #shader_tutorial 

![[water-drop.gif.gif]]

```glsl
#ifdef GL_ES
precision mediump float;
#endif

uniform vec2 u_resolution;
uniform float u_time;

// 1. A basic Signed Distance Field for a circle.
// Returns negative values inside the circle, positive outside, 0 at the edge.
float sdCircle(vec2 p, float r) {
  return length(p) - r;
}

void main() {
  // Normalize coordinates and center them (-1.0 to 1.0)
  vec2 st = gl_FragCoord.xy / u_resolution.xy;
  st = st * 2.0 - 1.0;

  // Correct aspect ratio so the droplet isn't stretched
  st.x *= u_resolution.x / u_resolution.y;

	float u_time = u_time * 1.1;

  // 2. Domain Warping
  // We distort the coordinate grid itself using time-based sine waves.
  vec2 warp;
  warp.x = sin(st.y * 6.0 + u_time) * 0.15;
  warp.y = cos(st.x * 5.0 + u_time * 1.2) * 0.1;

  // Add secondary high-frequency warping for surface tension ripples
  warp.x += sin(st.y * 15.0 - u_time * 2.0) * 0.02;

  // Apply the warp to our coordinates
  vec2 warped_st = st + warp;

  // 3. Calculate Distance
  // Pass the distorted coordinates into the perfect circle SDF
  float distance = sdCircle(warped_st, 0.4);

  // 4. Render the Boundary
  // Use smoothstep for anti-aliasing instead of a hard step
  float mask = smoothstep(0.01, -0.01, distance);

  // Apply color: A deep blue core with a lighter cyan edge
  vec3 dropletColor = mix(vec3(0.05, 0.4, 0.8), vec3(0.4, 0.8, 1.0), distance * 2.0 + 0.5);
  vec3 bgColor = vec3(0.05, 0.05, 0.08);

  vec3 finalColor = mix(bgColor, dropletColor, mask);

  gl_FragColor = vec4(finalColor, 1.0);
}

```