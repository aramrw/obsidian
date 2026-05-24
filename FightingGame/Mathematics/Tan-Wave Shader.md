#shaders #graphics #computer_graphics #computer_science #math #shader_tutorial

![[output3.gif|273]]

## Deconstructing the Tan-Wave Shader
- credit: https://www.shadertoy.com/view/wltSRS)

To port logic from [[Shadertoy]] to [[glslViewer]], the environment variables must be bridged. Shadertoy relies on `iResolution` and `iTime`. glslViewer natively utilizes `u_resolution` and `u_time`.

## 1. Core Mathematical Mechanics

Before manipulating pixels, the underlying forces dictating the coordinate space must be understood. Shaders transform the screen from a pixel grid into a mathematical plane.

- [[UV Normalization]]: 
- > $uv = \frac{\text{gl\_FragCoord.xy} - 0.5 \cdot \text{u\_resolution.xy}}{\text{u\_resolution.y}}$. This establishes $(0,0)$ at the center of the viewport, correcting for aspect ratio.
    
- [[Space Repetition]]: 
- > The fractional function isolates the decimal part of a number: $f(x) = x - \lfloor x \rfloor$. In GLSL, `fract(x)` creates an infinite repeating [[Space Repetition#Sawtooth]] wave from $0.0$ to $1.0$. This duplicates geometric data across the screen without requiring iterations or loops.
    
- [[Domain Warping]]:
- > Rather than drawing a complex shape, the coordinate space itself is distorted before a simple shape is drawn. The formula $x' = x + \tan(|x| \cdot 5)$ tears the grid outward from the center. _Note: Relying on a tangent curve for warping introduces mathematical asymptotes. This causes infinite stretching at regular intervals. While stylistically distinct, using a continuous function like $\sin(x)$ or `[[Simplex Noise]]` provides a more stable, artifact-free distortion._
    
- [[Smoothstep Interpolation]]: 
- > `smoothstep(edge0, edge1, x)` thresholds values, returning $0.0$ or $1.0$ while smoothly interpolating the boundary. It is the standard mechanism for rendering crisp, anti-aliased geometry.
    

## 2. Motion and Masking

The foundational step is rendering a moving boundary.

abs() = [[Absolute Value]]

```glsl
#ifdef GL_ES
precision mediump float;
#endif

uniform vec2 u_resolution;
uniform float u_time;

void main() {
    // Center and normalize coordinates
    vec2 uv = (gl_FragCoord.xy - 0.5 * u_resolution.xy) / u_resolution.y;

    float speed = u_time * 0.5;

    // abs() mirrors the line across the axis; smoothstep hardens the edge
    float line = smoothstep(0.02, 0.01, abs(uv.y + sin(speed) * 0.4));

    gl_FragColor = vec4(vec3(line), 1.0);
}
```

## 3. Color Context and Blending

Colors are 3D vectors representing Red, Green, and Blue channels, strictly bound between $0.0$ and $1.0$. See [[Color Generation]].

To apply color, use linear interpolation (`mix`) to dictate where the foreground and background exist based on the mask generated in the previous step.

**Language:** `glsl`

```glsl
#ifdef GL_ES
precision mediump float;
#endif

uniform vec2 u_resolution;
uniform float u_time;

void main() {
    vec2 uv = (gl_FragCoord.xy - 0.5 * u_resolution.xy) / u_resolution.y;

    float line_mask = smoothstep(0.02, 0.01, abs(uv.y + sin(u_time * 0.5) * 0.4));

    vec3 bg_color = vec3(0.1, 0.1, 0.1); 
    vec3 fg_color = vec3(0.2, 0.8, 0.4); 

    // Mix routes the bg and fg vectors based on the mask's binary state
    vec3 final_color = mix(bg_color, fg_color, line_mask);

    gl_FragColor = vec4(final_color, 1.0);
}
```

## 4. [[Color Modulation]]

Static colors are inefficient for dynamic visual systems. By modulating the color vectors based on pixel location (`uv.x`) and `u_time`, the color palette becomes an emergent property of the space.

```glsl
#ifdef GL_ES
precision mediump float;
#endif

uniform vec2 u_resolution;
uniform float u_time;

void main() {
    vec2 uv = (gl_FragCoord.xy - 0.5 * u_resolution.xy) / u_resolution.y;

    float clock = u_time / 5.0;
    float line_mask = smoothstep(0.02, 0.01, abs(uv.x));

    // Tangent function drives the intensity modulation
    float p = tan(uv.x + u_time);

    vec3 bg_color = vec3(0.1, 0.1, 0.1);

    // Red and blue channels fluctuate via stepped sine/cosine waves
    vec3 fg_color = vec3(
        p * 0.1 + step(0.1, abs(cos(clock * 2.0)) * uv.x), 
        p * 0.9, 
        0.1 + step(1.0, sin(clock) * sin(clock) * abs(uv.x))
    );

    vec3 final_color = mix(bg_color, fg_color, line_mask);

    gl_FragColor = vec4(final_color, 1.0);
}
```

## 5. Final Assembly: Warping and Quantization

The final logic discards the single line. It implements space repetition via `fract()` and tears the grid using domain warping. Additionally, alpha channels are quantized to create stepping artifacts.

```glsl
#ifdef GL_ES
precision mediump float;
#endif

uniform vec2 u_resolution;
uniform float u_time;

void main() {
    vec2 uv = (gl_FragCoord.xy - 0.5 * u_resolution.xy) / u_resolution.y;
    vec2 uuv = uv; // Preserve un-warped state for structural reference

    // Timing calculations
    float clock = u_time / 5.0;
    float ttime = floor(u_time) + pow(fract(u_time), sin(u_time * 1.333) * 0.5);

    // Domain Warping
    uv.x += tan(abs(uv.x) * 5.0);

    // Space Repetition
    float d = fract(10.0 * uv.x + clock);
    d = smoothstep(0.2, 0.10, d);

    // [[Color Generation]]
    float p = tan(uv.x + u_time);
    vec3 bg_color = vec3(0.1, 0.1, 0.1);
    vec3 fg_color = vec3(
        p * 0.1 + step(0.1, abs(cos(clock * 2.0)) * uv.x), 
        p * 0.9, 
        0.1 + step(1.0, sin(clock) * sin(clock) * abs(uv.x))
    );

    vec3 final_color = mix(bg_color, fg_color, d);

    // Alpha modulation based on quantized grid distance
    float alpha = d * sin(ttime + 1.0 - floor(length(floor(uuv * 10.0))));

    gl_FragColor = vec4(final_color, alpha);
}
```