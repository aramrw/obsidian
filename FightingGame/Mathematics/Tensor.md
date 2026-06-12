#math #machine-learning

# Tensor

In the context of the custom ML codebase, a `Tensor` is essentially a container for numerical data. 

While a [[Scalars|scalar]] is a single number, a [[Vectors|vector]] is a 1D list of numbers, and a [[Matrices|matrix]] is a 2D grid, a **Tensor** is a generalization of all these—it can be a multi-dimensional array of any size (1D, 2D, 3D, etc.).

In the `ml/src/main.rs` code, the `Tensor` struct is defined like this:

```rust
struct Tensor {
    // A flat 1D list of numbers that holds all the actual values.
    // Storing it flat is better for memory contiguity and performance.
    pub data: Vec<f32>,
    
    // The dimensions of the tensor (e.g., [rows, cols]). 
    // This gives 2D, 3D, or N-Dimensional structure to the flat `data` vector.
    pub shape: Vec<usize>,
}

impl Tensor {
    // Helper to initialize a matrix of zeros
    pub fn zeros(rows: usize, cols: usize) -> Self {
        Tensor {
            // Total elements = rows * cols
            data: vec![0.0; rows * cols],
            // Shape defined as 2D
            shape: vec![rows, cols],
        }
    }
}
```

Tensors are the standard way data (like images, text, or audio) and neural network parameters are stored and manipulated in Machine Learning.