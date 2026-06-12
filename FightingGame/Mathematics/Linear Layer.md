#machine-learning

# Linear Layer

In the ML codebase, this is implemented as the `LinearLayer` struct. In machine learning literature, it is often also called a **Dense Layer** or a **Fully Connected Layer**.

While a single [[Artificial Neuron]] (or `Detector`) can only output one score, a **Linear Layer** is a collection of multiple neurons working side-by-side. 

Because it has multiple neurons, its structure in Rust expands on the single `Detector`:

```rust
pub struct LinearLayer {
    // Instead of one list of weights, we have a matrix (a list of lists).
    // One row of weights for each output neuron we want to produce.
    // (In an optimized library, this would be a 2D Tensor).
    pub weights: Vec<Vec<f32>>,
    
    // One bias for each output neuron.
    pub biases: Vec<f32>,
}

impl LinearLayer {
    pub fn new(num_inputs: usize, num_outputs: usize) -> Self {
        LinearLayer {
            // Create `num_outputs` rows, each containing `num_inputs` weights
            weights: vec![vec![0.5; num_inputs]; num_outputs],
            // Create a bias for each output
            biases: vec![0.0; num_outputs],
        }
    }
    // ... (forward pass logic omitted here, see [[Forward Pass]])
}
```

When you pass data through a Linear Layer, every input signal is connected to *every* neuron in the layer. This allows the network to evaluate the exact same input for multiple different patterns or "rules" simultaneously, outputting a list of multiple scores instead of just one.