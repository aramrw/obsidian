#math #animation #shaders #gamedev

Interpolation is the mathematical method of constructing new data points within the range of a discrete set of known data points. In game development, it is the bridge between "state A" and "state B."

---

## 1. LERP (Linear Interpolation)

LERP follows a straight line between two values.

### The Math
$$\text{lerp}(a, b, t) = a(1 - t) + bt$$
*   **$a$**: Start value ($t=0$).
*   **$b$**: End value ($t=1$).
*   **$t$**: The interpolant (percentage). 

**Crucial Note:** In practice, $t$ should be **clamped** between $0$ and $1$ to prevent "overshooting" unless you specifically want **Extrapolation**.

> Note: Can be paired with the [[Step Function]] in [[OpenGL]] as binary switches (if without branching).

### Vectorized LERP
LERP isn't just for numbers; it works for Vectors ($vec2, vec3$) by interpolating each component individually.
```rust
// Vector LERP in Rust
impl Vec2 {
    pub fn lerp(a: Vec2, b: Vec2, t: f32) -> Vec2 {
        Vec2 {
            x: a.x + t * (b.x - a.x),
            y: a.y + t * (b.y - a.y),
        }
    }
}
```

---

## 2. Inverse Lerp & Remapping

These are the "secret weapons" of technical art and shader programming.

### Inverse Lerp (InvLerp)
If LERP gives you a value from a percentage, **InvLerp** gives you the percentage from a value.
$$\text{invLerp}(a, b, v) = \frac{v - a}{b - a}$$
*Example:* If a health bar is between 50 and 100, and current health is 75, `invLerp(50, 100, 75)` returns `0.5`.

### Remap
Takes a value from one range and maps it into another.
$$\text{remap}(a, b, c, d, v) = \text{lerp}(c, d, \text{invLerp}(a, b, v))$$

---

## 3. SLERP (Spherical Linear Interpolation)

Used for interpolating between directions or $[[Quaternions]]$. LERP on a rotation takes a "shortcut" through the center of the sphere, causing the rotation to speed up in the middle. SLERP moves along the **Great Circle** arc at a constant speed.

### The Formula
$$\text{slerp}(\mathbf{v_0}, \mathbf{v_1}, t) = \frac{\sin((1-t)\Omega)}{\sin \Omega}\mathbf{v_0} + \frac{\sin(t\Omega)}{\sin \Omega}\mathbf{v_1}$$
Where $\Omega$ is the angle between the vectors.

---

## 4. Nonlinear Interpolation (Easing)

To make movements feel organic, we modify the $t$ value before passing it to LERP.

### Quadratic Ease In (Accelerating)
$$t' = t^2$$
### Quadratic Ease Out (Decelerating)
$$t' = 1 - (1 - t)^2$$
### Smoothstep (The S-Curve)
Standard in shaders for smooth masks. It uses a cubic Hermite interpolation.
$$\text{smoothstep}(t) = 3t^2 - 2t^3$$

---

## 5. Shader Functions (GLSL)

### `mix(a, b, t)`
The GLSL name for LERP. It can mix colors, positions, or textures.

```glsl
// A simple color gradient over time
vec3 colorA = vec3(1.0, 0.0, 0.0); // Red
vec3 colorB = vec3(0.0, 0.0, 1.0); // Blue
float t = sin(u_time) * 0.5 + 0.5; // Oscillation between 0 and 1

vec3 finalColor = mix(colorA, colorB, t);
```

### `step(edge, x)` & `smoothstep(edge0, edge1, x)`
Used to create sharp or soft boundaries (masks).

```glsl
void main() {
    vec2 uv = gl_FragCoord.xy / u_resolution;

    // A sharp circle mask
    float mask_sharp = 1.0 - step(0.3, length(uv - 0.5));

    // A soft glow mask
    float mask_soft = 1.0 - smoothstep(0.2, 0.4, length(uv - 0.5));

    gl_FragColor = vec4(vec3(mask_soft), 1.0);
}
```

### The "Remap" Function (Custom)
Since GLSL doesn't have a built-in `remap`, we often implement it ourselves:

```glsl
float remap(float low1, float high1, float low2, float high2, float value) {
    return low2 + (value - low1) * (high2 - low2) / (high1 - low1);
}
```

---

---

## Related Concepts
* [[Quaternions]]
* [[Vectors]]
* [[Trigonometry]]
* [[Distance Functions]]
* [[Audio Processing]] (Envelopes like Attack/Decay use these curves)
