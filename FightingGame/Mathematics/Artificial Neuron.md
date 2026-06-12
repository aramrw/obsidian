#machine-learning

# Artificial Neuron (Detector)

In the ML codebase, this concept is implemented as the `Detector` struct. 

An Artificial Neuron (often called a Perceptron or a Node) is the fundamental building block of a neural network. Its job is to take multiple inputs, weigh their individual importance, and output a single "activation score".

Here is how it is structured in Rust:

```rust
pub struct Detector {
    // Think of these as "volume knobs" that tune how much attention 
    // the neuron should pay to each specific input signal.
    // In a deeper network, this would be a Tensor, but here it's a 1D Vector.
    pub weights: Vec<f32>,
    
    // A baseline starting score added to the output.
    pub bias: f32,
}

impl Detector {
    // Create a new detector with a specific number of input wires
    pub fn new(num_inputs: usize) -> Self {
        Detector {
            // Initialize all knobs to a neutral 0.5
            weights: vec![0.5; num_inputs],
            // Bias starts at a neutral 0.0
            bias: 0.0,
        }
    }
    // ... (forward pass logic omitted here, see [[Forward Pass]])
}
```

During a **[[Forward Pass]]**, the neuron takes the incoming signals and mathematically calculates the [[Dot Product]] with its weights. It multiplies each input by its corresponding weight, adds them all together along with the bias, and produces a final score. 

If the score is high enough, the neuron "fires" or detects whatever specific pattern it was designed to find.