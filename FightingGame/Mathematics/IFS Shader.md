#shaders #shader_tutorial 

![[Pasted image 20260527084713.png|201]]

```glsl
#version 120

uniform float u_time;
uniform vec2 u_resolution;

// Global variables for function communication
vec4 light;
float ui;
mat2 m, n, nn;

// Distance estimation function
float map(vec3 p) {
  // Distance to the light source sphere
  float d = length(p - light.xyz) - light.w;

  // Bounding plane limitation
  d = min(d, max(10.0 - p.z, 0.0));

  float t = 2.5;

  // Iterated Function System (IFS) fractal loop
  // To simplify the geometry for basic learning, comment out this loop block.
  for (int i = 0; i < 13; i++) {
    t = t * 0.5;
    p.xy = m * p.xy;
    p.yz = n * p.yz;
    p.zx = nn * p.zx;
    p.xz = abs(p.xz) - t;
  }

  d = min(d, length(p) - 1.4 * t);
  return d;
}

// Normal vector estimation via central differences
vec3 norm(vec3 p) {
  vec2 e = vec2(0.001, 0.0);
  return normalize(vec3(
      map(p + e.xyy) - map(p - e.xyy),
      map(p + e.yxy) - map(p - e.yxy),
      map(p + e.yyx) - map(p - e.yyx)
    ));
}

// Fixed-step raymarching engine
vec3 dive(vec3 p, vec3 d) {
  for (int i = 0; i < 20; i++) {
    p += d * map(p);
  }
  return p;
}

void main() {
  // Normalize fragment coordinates to [-1, 1] range and correct aspect ratio
  vec2 v = gl_FragCoord.xy / u_resolution.xy * 2.0 - 1.0;
  v.x *= u_resolution.x / u_resolution.y;

  // Scale time uniform
  ui = 10.0 * u_time;

  // Compute dynamic rotation matrices
  float y = -0.001 * ui;
  m = mat2(sin(y), cos(y), -cos(y), sin(y));

  y = 0.0035 * ui;
  n = mat2(sin(y), cos(y), -cos(y), sin(y));

  y = 0.0023 * ui;
  nn = mat2(sin(y), cos(y), -cos(y), sin(y));

  // Define camera ray origin and light properties
	float zoom = 15;
  vec3 r = vec3(0.0, 0.0, -zoom + 10.0 * sin(0.001 * ui));
  light = vec4(10.0 * sin(0.01 * ui), 2.0, -23.0, 1.0);

  // Establish ray direction
  vec3 d = normalize(vec3(v, 5.0));

  // Execute primary surface intersection search
  vec3 p = dive(r, d);

  // Compute surface details and vectors
  d = normalize(light.xyz - p);
  vec3 no = norm(p);
  vec3 col = vec3(0.7, 0.8, 0.9);

  // Execute secondary shadow-ray intersection search
  vec3 bounce = dive(p + 0.01 * d, d);

  // Apply diffuse shading based on surface normal orientation
  col = mix(col, vec3(0.0), dot(no, normalize(light.xyz - p)));

  // Occlude color if secondary ray encounters an obstruction prior to the light source
  if (length(bounce - light.xyz) > light.w + 0.1) {
    col *= 0.2;
  }

  // Set final fragment output color
  gl_FragColor = vec4(col, 1.0);
}

```