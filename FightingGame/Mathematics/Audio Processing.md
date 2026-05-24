#math #audio #waves #trigonometry

Sound, at its physical core, is a wave of pressure moving through a medium. Circular functions (Sine and Cosine) are the mathematical language used to describe, generate, and manipulate these waves.

---

## 1. The Projection of Circular Motion

A circular function tracks a single point moving around a circle at a constant speed. Plotting the vertical position (y-coordinate) against time generates a sine wave.

In physics, this is **Simple Harmonic Motion**. When a string vibrates or a speaker cone moves, it mirrors this geometric projection.

$$\sin(\theta)$$

A pure sine wave represents the simplest possible sound: a single frequency with no overtones.

---

## 2. Building Complex Sound (Fourier Theory)

Any complex, periodic sound can be represented as a sum of simple sine and cosine waves with different frequencies, amplitudes, and phases. This is **Fourier Analysis**.

*   **Fundamental Frequency:** Determines the perceived pitch.
*   **Harmonics:** Integer multiples ($2f, 3f...$) that determine the **timbre** (tonal quality).

### Example: Square Wave Formula
A square wave is constructed by adding only odd harmonics to a fundamental:

$$f(t) = \frac{4}{\pi} \sum_{n=1,3,5...}^{\infty} \frac{1}{n} \sin(n\omega t)$$

---

## 3. Digital Signal Processing (DSP)

DSP is the translation of continuous waves into discrete numbers.

### Sampling (Nyquist-Shannon)
To perfectly reconstruct a signal, the sampling rate must be twice the highest frequency. Standard audio uses 44.1 kHz to capture the human range (20 Hz - 20 kHz). See [[Nyquist-Shannon Theorem]].

### Phase and Cancellation
Circular functions depend on angles (radians). Shifting the starting angle alters the **phase**. 

If two identical signals are $180^\circ$ ($\pi$ radians) out of phase, they perfectly oppose each other, resulting in **Phase Cancellation**. This is the core mechanic of **Active Noise Cancellation (ANC)**.

### Convolution and Filtering
Convolution is used to apply filters (EQ) or simulate physical spaces (Reverb) by combining a signal with an **Impulse Response**. See [[Convolution]].

### Sine Wave Oscillator (Rust)
```rust
pub struct Oscillator {
    pub sample_rate: f32,
    pub frequency: f32,
    phase: f32,
}

impl Oscillator {
    pub fn next_sample(&mut self) -> f32 {
        let sample = self.phase.sin();
        // Advance phase based on frequency and sample rate
        self.phase += 2.0 * std::f32::consts::PI * self.frequency / self.sample_rate;
        // Keep phase within [0, 2pi]
        if self.phase > 2.0 * std::f32::consts::PI {
            self.phase -= 2.0 * std::f32::consts::PI;
        }
        sample
    }
}
```

---

## 4. Active Noise Cancellation Constraints

While $1 + (-1) = 0$ works in math, physical silence is limited by:

1.  **Latency:** The inverted wave must hit the eardrum at the exact same millisecond as the noise. High-frequency drift can actually amplify noise if latency is too high.
2.  **Wavelength:**
    *   **Low Frequencies:** Long wavelengths (feet). Small discrepancies in position matter less, making engines easy to cancel.
    *   **High Frequencies:** Short wavelengths (centimeters). Fractional misalignment leads to constructive interference (louder noise).
3.  **Feedforward vs. Feedback:**
    *   **Feedforward:** External mic catches noise early (good for high-freq).
    *   **Feedback:** Internal mic listens to what you hear (good for low-freq rumbles).

---

## Related Concepts
* [[Trigonometry]] (Circular functions)
* [[Interpolation]] (Smoothing signals)
* [[Complex Numbers]] (Fast Fourier Transforms)
* [[GLSL Shaders]] (Visualizing waves)
* [[Nyquist-Shannon Theorem]]
* [[Convolution]]
