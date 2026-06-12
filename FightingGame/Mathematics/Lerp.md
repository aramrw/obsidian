```rust
use rand; // 0.10.1
use rand::prelude::*;

fn linear_interpolate(data: &[f32], position: f32) -> f32 {
    // Find the indices immediately below and above the position
    let index_lower = position.floor() as usize;
    let index_upper = (index_lower + 1).min(data.len() - 1);

    let a = data[index_lower];
    let b = data[index_upper];

    // Extract only the fractional part to act as our weight 't' (e.g., 2.8 becomes 0.8)
    let weight = position.fract(); 

    // Apply the lerp equation
    a + weight * (b - a)
}

fn main() {
   let mut data = vec![];
   let mut rng = rand::rng();
   for i in 0..10 {
      let rn = rng.random_range(0.0..=1.); 
      data.push(rn);
   }
   dbg!(&data);
   
  let weight = linear_interpolate(&data, 2.0);
  dbg!(weight);
   
}
```

```rust
[src/main.rs:26:4] &data = [
    0.50696564,
    0.0036437511,
    0.3852625,
    0.5735767,
    0.54588056,
    0.83162475,
    0.31217062,
    0.6923293,
    0.004014492,
    0.9549358,
]
[src/main.rs:29:3] weight = 0.3852625
```