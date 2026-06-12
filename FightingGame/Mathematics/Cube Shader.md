#shader_tutorial #shaders #raytracing #raymarching

![[Pasted image 20260526120930.png|197]]

[[RayMarching]]

```glsl
#ifdef GL_ES
precision mediump float;
#endif

uniform vec2 u_resolution;
uniform float u_time;

// 1. Signed Distance Field for a 3D Box
float sdBox(vec3 p, vec3 b) {
  vec3 q = abs(p) - b;
  return length(max(q, 0.0)) + min(max(q.x, max(q.y, q.z)), 0.0);
}

// Simple rotation function to turn a 2D plane by an angle
vec2 rotate2D(vec2 p, float angle) {
  float s = sin(angle);
  float c = cos(angle);
  return vec2(p.x * c - p.y * s, p.x * s + p.y * c);
}

// 2. Calculate the surface normal at point 'p'
vec3 getNormal(vec3 p) {
  vec2 e = vec2(0.001, 0.0);
  vec3 b = vec3(0.8); // Must match the box size in main()

  float nx = sdBox(p + e.xyy, b) - sdBox(p - e.xyy, b);
  float ny = sdBox(p + e.yxy, b) - sdBox(p - e.yxy, b);
  float nz = sdBox(p + e.yyx, b) - sdBox(p - e.yyx, b);

  return normalize(vec3(nx, ny, nz));
}

void main() {
  // Normalize screen coordinates (-1.0 to 1.0) and fix aspect ratio
  vec2 st = gl_FragCoord.xy / u_resolution.xy;
  st = st * 2.0 - 1.0;
  st.x *= u_resolution.x / u_resolution.y;

  // --- 3D RAYMARCHING SETUP ---
  vec3 rayOrigin = vec3(0.0, 0.0, 5.0);
  vec3 rayDirection = normalize(vec3(st.x, st.y, -1.0));

  // --- TILT THE CAMERA ---
  rayOrigin.yz = rotate2D(rayOrigin.yz, 0.5);
  rayDirection.yz = rotate2D(rayDirection.yz, 0.5);
  rayOrigin.xz = rotate2D(rayOrigin.xz, 0.6);
  rayDirection.xz = rotate2D(rayDirection.xz, 0.6);

  float totalDistance = 0.0;
  float hit = 0.0;
  vec3 hitPos = vec3(0.0);

  // --- THE MARCHING LOOP ---
  for (int i = 0; i < 64; i++) {
    vec3 currentPos = rayOrigin + rayDirection * totalDistance;
    float safeStep = sdBox(currentPos, vec3(0.8));

    if (safeStep < 0.001) {
      hit = 1.0;
      hitPos = currentPos;
      break;
    }

    if (totalDistance > 15.0) {
      break;
    }

    totalDistance += safeStep;
  }

  // --- RENDER ---
  vec3 bgColor = vec3(0.01, 0.01, 0.01);
  vec3 finalColor = bgColor;

  if (hit > 0.5) {
    vec3 normal = getNormal(hitPos);
    vec3 cubeColor = vec3(1.0); // Fallback color

    // Isolate each face using the direction of the normal vector
    if (normal.x > 0.5) {
      cubeColor = vec3(0.9, 0.2, 0.2); // Right face: Red
    } else if (normal.x < -0.5) {
      cubeColor = vec3(0.2, 0.9, 0.2); // Left face: Green
    } else if (normal.y > 0.5) {
      cubeColor = vec3(0.2, 0.2, 0.9); // Top face: Blue
    } else if (normal.y < -0.5) {
      cubeColor = vec3(0.9, 0.9, 0.2); // Bottom face: Yellow
    } else if (normal.z > 0.5) {
      cubeColor = vec3(0.9, 0.2, 0.9); // Front face: Magenta
    } else if (normal.z < -0.5) {
      cubeColor = vec3(0.2, 0.9, 0.9); // Back face: Cyan
    }

    finalColor = cubeColor;
  }

  gl_FragColor = vec4(finalColor, 1.0);
}
```

# Details

### abs(vec3)


```glsl
float sdBox(vec3 p, vec3 b) {
  vec3 q = abs(p) - b;
  return length(max(q, 0.0)) + min(max(q.x, max(q.y, q.z)), 0.0);
}
```

In the `sdBox` function you used above, `abs(p)` is the magic trick that folds 3D space.

Instead of writing 8 different math formulas to calculate the distance to the 8 different corners of the cube, **`abs(p)` forces any coordinate in negative space (left, down, or back) into the positive octant (right, up, and forward)**. This lets the shader calculate the distance to just **one corner**, and it instantly applies to all 8 corners of the cube (since they are all equal).

# Final Code With Lighting

[[RayMarching#How to implement it in your code]]

```glsl
#ifdef GL_ES
precision mediump float;
#endif

uniform vec2 u_resolution;
uniform float u_time;
uniform vec2 u_mouse; // Vector containing mouse X and Y coordinates

// 1. Signed Distance Field for a 3D Box
float sdBox(vec3 p, vec3 b) {
  vec3 q = abs(p) - b;
  return length(max(q, 0.0)) + min(max(q.x, max(q.y, q.z)), 0.0);
}

// Simple rotation function to turn a 2D plane by an angle
vec2 rotate2D(vec2 p, float angle) {
  float s = sin(angle);
  float c = cos(angle);
  return vec2(p.x * c - p.y * s, p.x * s + p.y * c);
}

// 2. Calculate the surface normal at point 'p'
vec3 getNormal(vec3 p, vec3 box_size) {
  vec2 e = vec2(0.001, 0.0);
  vec3 b = vec3(box_size);

  float nx = sdBox(p + e.xyy, b) - sdBox(p - e.xyy, b);
  float ny = sdBox(p + e.yxy, b) - sdBox(p - e.yxy, b);
  float nz = sdBox(p + e.yyx, b) - sdBox(p - e.yyx, b);

  return normalize(vec3(nx, ny, nz));
}

void main() {
  // Normalize screen coordinates (-1.0 to 1.0) and fix aspect ratio
  vec2 st = gl_FragCoord.xy / u_resolution.xy;
  st = st * 2.0 - 1.0;
  st.x *= u_resolution.x / u_resolution.y;

  // Normalize mouse coordinates (-1.0 to 1.0)
  vec2 mouse = u_mouse.xy / u_resolution.xy;
  mouse = mouse * 2.0 - 1.0;

  // --- 3D RAYMARCHING SETUP ---
  vec3 rayOrigin = vec3(0.0, 0.0, 3.0);
  vec3 rayDirection = normalize(vec3(st.x, st.y, -1.0));

  // --- MOUSE CAMERA ROTATION ---
  // Pitch: Rotate around the X-axis (up/down) using mouse Y
  float pitch = mouse.y * 1.57; // Limit vertical rotation to ~90 degrees
  rayOrigin.yz = rotate2D(rayOrigin.yz, pitch);
  rayDirection.yz = rotate2D(rayDirection.yz, pitch);

  // Yaw: Rotate around the Y-axis (left/right) using mouse X
  float yaw = mouse.x * 3.14; // Allow 180 degree horizontal rotation
  rayOrigin.xz = rotate2D(rayOrigin.xz, yaw);
  rayDirection.xz = rotate2D(rayDirection.xz, yaw);

  float totalDistance = 0.0;
  float hit = 0.0;
  vec3 hitPos = vec3(0.0);

  vec3 box_size = vec3(0.8);

  // --- THE MARCHING LOOP ---
  for (int i = 0; i < 64; i++) {
    vec3 currentPos = rayOrigin + rayDirection * totalDistance;
    float safeStep = sdBox(currentPos, box_size);

    if (safeStep < 0.001) {
      hit = 1.0;
      hitPos = currentPos;
      break;
    }

    if (totalDistance > 15.0) {
      break;
    }

    totalDistance += safeStep;
  }

  // --- RENDER ---
  vec3 bgColor = vec3(0.01, 0.01, 0.01);
  vec3 finalColor = bgColor;

  if (hit > 0.5) {
    vec3 normal = getNormal(hitPos, box_size);
    vec3 baseColor = vec3(0.4, 0.5, 0.5);

    // Light source moves with the camera origin
    vec3 lightPos = rayOrigin;
    vec3 lightDir = normalize(lightPos - hitPos);

    float diffuse = max(dot(normal, lightDir), 0.0);
    float ambient = 0.05;
    float lightIntensity = diffuse + ambient;

    finalColor = baseColor * lightIntensity;
  }

  gl_FragColor = vec4(finalColor, 1.0);
}
```