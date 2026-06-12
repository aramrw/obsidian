#machine-learning #codebase

# ML Codebase Overview

This note provides an overview of the custom Machine Learning codebase written in Rust (located in `ml/src/main.rs`). The code is a foundational implementation of a neural network from scratch.

It consists of three main structural components:

1. **[[Tensor]]**: The underlying data structure for doing math with multiple dimensions of data.
2. **`Detector` ([[Artificial Neuron]])**: The smallest decision-making unit (a single neuron).
3. **`LinearLayer` ([[Linear Layer]])**: A collection of multiple detectors working together simultaneously.

### How it works
The `main()` function tests these components by performing a **[[Forward Pass]]** to generate predictions based on its tunable **[[Weights and Biases]]**:

```rust
fn main() {
    // 1. We have 3 input letters, so we need a detector with 3 "volume knobs"
    let detector_a = Detector::new(3);

    // 2. The incoming signal: 'm', 'o', 's' represented as numbers
    let incoming_signal = vec![1.0, 2.0, 3.0];

    // 3. Run the signal through the single detector
    let final_score = detector_a.forward(&incoming_signal);
    println!("Detector A's final activation score is: {}", final_score);

    // 4. Instead of one detector, create a layer that outputs 2 scores simultaneously
    // (e.g., predicting Rule 1 or Rule 2)
    let layer = LinearLayer::new(3, 2);
    let layer_scores = layer.forward(&incoming_signal);
    println!("Linear Layer scores: {:?}", layer_scores);
}
```