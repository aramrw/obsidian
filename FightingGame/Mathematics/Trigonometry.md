#math #trigonometry #waves #computer_graphics 

# Traveling Wave Equation

The traveling wave equation describes a sinusoidal wave moving through space over time.

$$y = A \sin(kx - \omega t) + D$$

## 1. Variables Breakdown

| Variable | Name | Description |
| :--- | :--- | :--- |
| **$y(x, t)$** | **Displacement** | The vertical position at position $x$ and time $t$. |
| **$A$** | **Amplitude** | The maximum displacement from equilibrium (peak height). |
| **$k$** | **Wave Number** | Spatial frequency; determines wave cycles over a unit distance. Defined as $k = \frac{2\pi}{\lambda}$ (where $\lambda$ is wavelength). |
| **$x$** | **Position** | The horizontal coordinate. |
| **$\omega$** | **Angular Frequency** | Temporal frequency; determines oscillation speed over time. Defined as $\omega = 2\pi f = \frac{2\pi}{T}$ (where $f$ is frequency, $T$ is period). |
| **$t$** | **Time** | The elapsed time. |
| **$D$** | **Vertical Shift** | The equilibrium position or vertical offset (DC offset). |

---

## 2. Practical Application: GLSL Shaders

In computer graphics, these formulas are frequently used to create animated effects like water ripples, waving grass, or moving lines.

### Example 1: Animated Sine Line
This shader uses the wave equation to calculate the "target height" for a horizontal pixel, then draws a line at that height.

```glsl
#version 120

uniform vec2 u_resolution;
uniform float u_time;

void main() {
    vec2 uv = gl_FragCoord.xy / u_resolution;

    // Mapping to the formula: y = A * sin(kx - wt) + D
    // A (Amplitude)         = 0.2
    // k (Wave Number)       = 1.0
    // w (Angular Frequency) = 10.0
    // D (Vertical Shift)    = 0.5
    float wave = sin(uv.x * 1.0 - u_time * 10.0) * 0.2 + 0.5;

    // Check how close current pixel's Y is to the wave height
    float distance_to_wave = abs(uv.y - wave);

    // Create a sharp line mask (1.0 inside thickness, 0.0 outside)
    float line = 1.0 - step(0.01, distance_to_wave);

    gl_FragColor = vec4(vec3(line), 1.0);
}
```

### Example 2: The Tangent Wave (Infinite Spikes)
While `sin` and `cos` are bounded between -1 and 1, `tan` approaches infinity as it hits its asymptotes ($\pi/2, 3\pi/2...$). In shaders, this creates distinct vertical "bars" or spikes.

```glsl
void main() {
    vec2 uv = gl_FragCoord.xy / u_resolution;

    // A tangent wave creates repeating vertical patterns
    float wave = tan(uv.x * 2.0 - u_time * 2.0) * 0.1 + 0.5;

    float dist = abs(uv.y - wave);
    float line = 1.0 - step(0.01, dist);

    gl_FragColor = vec4(vec3(line), 1.0);
}
```


---

## 3. Related Concepts
* [[Periodic Functions]]
* [[Fourier Transform]]
* [[Interpolation]] (smoothstep/step)
* [[Audio Processing]] (Sine waves and ANC)
* [[Affine Transformations]] (Rotations)
* [[Complex Numbers]] (using Euler's formula $e^{ix} = \cos x + i \sin x$ to represent waves)
* [[GLSL Shaders]]
