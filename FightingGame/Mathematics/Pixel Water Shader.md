#shaders #graphics #computer_graphics #computer_science #math #shader_tutorial

![[Pasted image 20260524105217.png|225]]

```glsl
#ifdef GL_ES
precision mediump float;
#endif

// glslViewer standard uniforms
uniform vec2 u_resolution;
uniform float u_time;

void main() {
    // 1. Normalize coordinates
    vec2 st = gl_FragCoord.xy / u_resolution.xy;

    // 2. Pixelate the UV coordinates
    // Lowering the multiplier increases the size of the "pixels"
    float pixelResolution = 64.0;
    vec2 pixel_st = floor(st * pixelResolution) / pixelResolution;

    // 3. Generate wave patterns using time and snapped coordinates
    float time = u_time * 1.5;
    vec2 wavePos = pixel_st * 8.0;

    // Combine overlapping sine/cosine waves for natural variation
    float wave1 = sin(wavePos.x + time) * cos(wavePos.y + time);
    float wave2 = sin(wavePos.x * 2.0 - time * 0.5) * cos(wavePos.y * 2.0 + time * 0.8);
    float totalWave = wave1 + wave2;

    // 4. Define a strict, retro color palette
    vec3 deepWater    = vec3(0.08, 0.28, 0.55);
    vec3 midWater     = vec3(0.15, 0.45, 0.75);
    vec3 shallowWater = vec3(0.30, 0.65, 0.85);
    vec3 foam         = vec3(0.85, 0.95, 0.98);

    // 5. Quantize the waves into flat color bands
    vec3 finalColor = deepWater;

    if (totalWave > 0.8) {
        finalColor = foam;
    } else if (totalWave > 0.2) {
        finalColor = shallowWater;
    } else if (totalWave > -0.4) {
        finalColor = midWater;
    }

    gl_FragColor = vec4(finalColor, 1.0);
}

```