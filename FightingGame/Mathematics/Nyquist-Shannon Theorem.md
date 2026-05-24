#math #audio #dsp

The Nyquist-Shannon sampling theorem is a bridge between continuous-time signals (analog sound) and discrete-time signals (digital data).

---

## 1. The Theorem

To perfectly reconstruct a signal without losing information, the **sampling frequency ($f_s$)** must be greater than twice the **maximum frequency ($f_{max}$)** present in the signal.

$$f_s > 2 \cdot f_{max}$$

*   **Nyquist Rate:** The minimum sampling rate required ($2 \cdot f_{max}$).
*   **Nyquist Frequency:** Half of the sampling rate ($f_s / 2$). This is the highest frequency a digital system can accurately represent.

---

## 2. Why 44.1 kHz?

Human hearing generally stops at $20,000 \text{ Hz}$.
- According to the theorem, we need at least $40,000 \text{ Hz}$ to capture the full human range.
- $44.1 \text{ kHz}$ provides a small "buffer zone" for **Anti-Aliasing Filters** to roll off high frequencies before they reach the Nyquist limit.

---

## 3. Aliasing

If a signal contains frequencies higher than the Nyquist frequency, they are "folded back" into the audible range as digital distortion called **aliasing**.

In audio, this sounds like metallic, unnatural noise. In graphics (shaders), this appears as "jaggies" on edges or Moire patterns.

### Anti-Aliasing (AA)
To prevent aliasing, we must filter out all frequencies above the Nyquist limit *before* sampling.

---

## Related Concepts
* [[Audio Processing]]
* [[Trigonometry]] (Wave reconstruction)
* [[GLSL Shaders]] (Spatial aliasing in textures)
