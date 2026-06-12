#machine-learning

# Forward Pass

In the codebase, this concept is represented by the `forward()` methods on the `Detector` and `LinearLayer` structs.

A **Forward Pass** (or Forward Propagation) is the process of taking input data and pushing it sequentially through the neural network from start to finish to get a prediction or score.

Mathematically, it involves calculating the [[Dot Product]] between the incoming input signals and the neuron's [[Weights and Biases|Weights]], and then adding the [[Weights and Biases|Bias]]. 

Here is how it is implemented in Rust. Notice how it iteratively calculates the [[Dot Product]]:

```rust
impl Detector {
    pub fn forward(&self, inputs: &[f32]) -> f32 {
        // 1. Start the score with our baseline bias
        let mut score = self.bias;

        // 2. Loop through the input signals and their corresponding volume knobs (weights)
        for (i, input_signal) in inputs.iter().enumerate() {
            // 3. Multiply the signal by the weight and add to the total (Dot Product)
            score += input_signal * self.weights[i];
        }

        // The final activation value
        score
    }
}
```

For a `LinearLayer`, the process is identical, but nested so it computes the dot product for *every* neuron in the layer:

```rust
impl LinearLayer {
    pub fn forward(&self, inputs: &[f32]) -> Vec<f32> {
        // Pre-allocate the output scores
        let mut output_scores = vec![0.0; self.biases.len()];

        // Loop over each "detector" (output node) in the layer
        for (out_idx, out_score) in output_scores.iter_mut().enumerate() {
            let mut score = self.biases[out_idx];

            // Loop over inputs for this specific detector
            for (in_idx, input_signal) in inputs.iter().enumerate() {
                score += input_signal * self.weights[out_idx][in_idx];
            }

            *out_score = score;
        }

        output_scores // Returns a vector of scores, one for each neuron
    }
}
```

It is considered "forward" because the data flows strictly in one direction: from input to output.