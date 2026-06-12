#shaders #math #vectors #vector #shader_tutorial 

![[Pasted image 20260525214600.png|146]]

```glsl
#version 120

uniform vec2 u_resolution;
uniform float u_time;

// Function to calculate the shortest distance from a pixel to a line segment
float distanceToLineSegment(vec2 p, vec2 a, vec2 b) {
  vec2 pa = p - a;
  vec2 ba = b - a;

  // Project pixel point onto the line segment, clamping between 0.0 and 1.0
  float h = clamp(dot(pa, ba) / dot(ba, ba), 0.0, 1.0);

  // Return the distance from the pixel to the closest point on the segment
  return length(pa - ba * h);
}

void main() {
  // Normalize coordinates so (0,0) is bottom-left and (1,1) is top-right
  vec2 st = gl_FragCoord.xy / u_resolution.xy;

  // Define line endpoints (keeping them inside the 0.0 to 1.0 visible range)
  vec2 bl = vec2(0.2, 0.2);
  vec2 tr = vec2(0.8, 0.8);
  vec2 br = vec2(0.8, 0.2);
  vec2 tl = vec2(0.2, 0.8);

  // Get the shortest distance from this specific pixel to the line
  float dist = distanceToLineSegment(st, bl, tr);
  float dist_side = distanceToLineSegment(st, tr, br);
  float dist_btm = distanceToLineSegment(st, bl, br);
  float tr_tl = distanceToLineSegment(st, tr, tl);
  float ls = distanceToLineSegment(st, tl, bl);

  // Set line thickness (e.g., 0.01 units wide)
  float thickness = 0.01;

  // If the distance is less than the thickness, color it white (1.0). Otherwise black (0.0).
  // smoothstep creates clean, anti-aliased edges instead of jagged pixels.
	float final = min(dist, dist_side);
	final = min(dist_btm, final);
	final = min(tr_tl, final);
	final = min(ls, final);
  float lineIntensity = 1.0 - smoothstep(thickness, thickness + 0.005, final);

  // Output the final color (White line on a black background)
  gl_FragColor = vec4(vec3(lineIntensity), 1.0);
}

```