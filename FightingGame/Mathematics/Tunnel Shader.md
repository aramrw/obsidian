#shader_tutorial 

![[tunnel.gif.gif|279]]

```glsl
#version 120

uniform float u_time;
uniform vec2 u_resolution;

// --- Configuration Constants ---
const int MAX_STEPS = 100; // Quality: Defines the depth of the raymarching. Higher = sharper, slower.
const float MOVEMENT_SPEED = 15.0; // Speed: Multiplier for forward traversal through the tunnel.
const float PULSE_SPEED = 5.0; // Speed: Multiplier for the wisp animation.

// Custom tanh implementation for GLSL 1.20 tone mapping
vec4 toneMap(vec4 color) {
  vec4 exp2x = exp(2.0 * color);
  return (exp2x - 1.0) / (exp2x + 1.0);
}

// Evaluates a scaled gyroid field
float getGyroidDistance(vec4 pos, float scale) {
  pos *= scale;
  // zxwy is a swizzle to offset the cosine terms against the sine terms
  return abs(dot(sin(pos), cos(pos.zxwy)) - 1.0) / scale;
}

void main() {
  vec2 fragCoord = gl_FragCoord.xy;
  vec2 resolution = u_resolution.xy;
  float time = u_time * PULSE_SPEED;

  float totalDistance = 0.0;
  float surfaceDistance = 0.0;
  float foldSign = 0.0;

  vec4 glowColor = vec4(0.0);
  vec4 rayPosition = vec4(0.0);
  vec4 localPos = vec4(0.0);

  // Base color vector used for procedural coloring
  vec4 colorPalette = vec4(2.0, 1.0, 0.0, 3.0);

  for (int i = 0; i < MAX_STEPS; ++i) {
    // Advance ray. The small epsilon prevents dividing by zero and creates translucency.
    totalDistance += surfaceDistance + 5.0e-4;

    // Calculate current ray position in 3D space
    vec3 rayDirection = normalize(vec3(fragCoord - 0.5 * resolution, resolution.y));
    rayPosition = vec4(rayDirection * totalDistance, 0.2);

    // Move forward through the tunnel
    rayPosition.z += (u_time / 30.0) * MOVEMENT_SPEED;

    // Fold space across the Y axis to create a mirror/water effect at the bottom
    foldSign = rayPosition.y + 0.1;
    rayPosition.y = abs(foldSign);

    localPos = rayPosition;
    localPos.y -= 0.11;

    // Twist the tunnel based on depth (Z axis)
    vec4 rotationAngles = vec4(0.0, 11.0, 33.0, 0.0) - 2.0 * localPos.z;
    vec4 cosAngles = cos(rotationAngles);
    mat2 twistMatrix = mat2(cosAngles.x, cosAngles.y, cosAngles.z, cosAngles.w);
    localPos.xy = twistMatrix * localPos.xy;

    localPos.y -= 0.2;

    // Sample two nested gyroids for complex structural detail
    surfaceDistance = abs(getGyroidDistance(localPos, 8.0) - getGyroidDistance(localPos, 24.0)) / 4.0;

    // Procedural color mapped along the Z axis
    vec4 stepColor = 1.0 + cos(0.7 * colorPalette + 5.0 * rayPosition.z);

    // Accumulate volumetric glow
    float reflectionDimmer = (foldSign > 0.0) ? 1.0 : 0.1;
    float distanceFalloff = max((foldSign > 0.0) ? surfaceDistance : surfaceDistance * surfaceDistance * surfaceDistance, 5.0e-4);

    glowColor += reflectionDimmer * stepColor.w * stepColor / distanceFalloff;
  }

  // Add the central pulsing wisp
  float pulse = 1.4 + sin(time) * sin(1.7 * time) * sin(2.3 * time);
  glowColor += pulse * 1000.0 * colorPalette / length(rayPosition.xy);

  // Apply tone mapping and output
  gl_FragColor = toneMap(glowColor / 100000.0);
}
```

## Geometry

> In this shader, the shape is a [[Gryoid]]. A [[Gryoid]] is an infinitely connected periodic minimal surface. It contains no straight lines and repeats infinitely in all directions. The core approximation of a gyroid is defined mathematically as:

$$\sin(x)\cos(y) + \sin(y)\cos(z) + \sin(z)\cos(x) = 0$$

The shader uses the `g()` function to calculate the distance to this infinite web of tunnels. 

```glsl
float g(vec4 p, float s) {
  p *= s;
  return abs(dot(sin(p), cos(p.zxwy)) - 1.0) / s;
}
```

By layering two gyroids of different scales (`g(p,8.) - g(p,24.)`), the author creates the intricate, organic texture on the cave walls.

```glsl
p: vec4;
d = abs(g(p, 8.0) - g(p, 24.0)) / 4.0;
```

## [[Domain Warping]]

You do not need to model an entire tunnel. You only need to model a small segment and manipulate the coordinate space to trick the ray into thinking the space is infinite or curved.

- **Mirroring (Folding):** 
- `q.y = abs(s)`: takes the entire world and mirrors it across an axis. 
- This creates the symmetrical "water reflection" effect at the bottom of the screen.
    
- **Twisting:** As the ray moves deeper into the tunnel (the Z-axis), the space is rotated along the X and Y axes. The deeper you go, the more the space rotates. This is what turns a straight, infinitely repeating gyroid structure into a winding, twisting cave.

## 4. Volumetric Accumulation: The Glow

A standard [[RayMarching|RayMarcher]] stops when it hits a surface and returns a solid color (e.g., rock). This shader never technically draws a solid surface.

Instead of stopping, the ray continues to step. At every step, it checks how close it is to the gyroid surface. If it is very close, it adds a bright color value to a running total (`o += ...`). If it is far away, it adds a dim color. This volumetric accumulation is what creates the ethereal, translucent "wisp" and the glowing cave walls. It is drawing the air _around_ the math, rather than the math itself.

## [[Phase (Waves)|Phase Shifting]]

```glsl
vec4 rotationAngles = vec4(0.0, 11.1, 33.0, 0.0) - 2.0 * localPos.z;
vec4 cosAngles = cos(rotationAngles);
```

Approximated the rotation instead of using sin by using [[Phase (Waves)|Phase Shifting]]
