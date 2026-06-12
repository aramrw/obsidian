
#shaders #math #vectors #vector #shader_tutorial 

![[Pasted image 20260526010832.png|155]]

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

float distance_formula(vec2 p, vec2 center) {
	float x = p.x - center.x;
	float y = p.y - center.y;
	return sqrt((x*x) + (y*y));
}

void main() {
  // Normalize coordinates so (0,0) is bottom-left and (1,1) is top-right
  vec2 st = (gl_FragCoord.xy / u_resolution.xy);

	vec2 circle_center = vec2(0.5, 0.5);
	float circle_radius = 0.3;

	float sd = distance_formula(st, circle_center) - circle_radius;
	// the circle line
	float abs_sd = abs(sd);
  float thickness = 0.01;
	// outside

  float bg_mask = smoothstep(sd, thickness + 0.005, abs_sd);

  // Output the final color (White line on a black background)
  gl_FragColor = vec4(vec3(bg_mask), 1.0);
}

```