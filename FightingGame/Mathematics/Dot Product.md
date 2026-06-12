https://en.wikipedia.org/wiki/Dot_product

#math #linear_algebra #rust

The **dot product** (or scalar product) is an algebraic operation that takes two equal-length sequences of numbers (usually coordinate vectors) and returns a single scalar value.

## 1. Mathematical Definition

The dot product of two vectors $\mathbf{a} = [a_1, a_2, \dots, a_n]$ and $\mathbf{b} = [b_1, b_2, \dots, b_n]$ is defined as:

$$\mathbf{a} \cdot \mathbf{b} = \sum_{i=1}^{n} a_i b_i = a_1 b_1 + a_2 b_2 + \dots + a_n b_n$$

---

### Idiomatic Rust Implementation

In Rust, calculating a dot product using raw arrays or slices looks exactly like the mathematical formula when you use `.iter()`, `.zip()`, and `.sum()`:

> [[Sigma Σ]]

```rust
fn dot_product(a: &[f32], b: &[f32]) -> f32 {
    assert_eq!(a.len(), b.len(), "Vectors must be of equal length");
    
    // This is exactly what the Sigma (∑) operator does:
    a.iter()
     .zip(b.iter())
     .map(|(ai, bi)| ai * bi)
     .sum()
}

fn main() {
    let a = [1.0, 3.0, -5.0];
    let b = [4.0, -2.0, -1.0];
    
    let result = dot_product(&a, &b);
    println!("Dot Product: {}", result); // Output: 3.0
}
```

### **# Usecases**

**General Geometry**

- **Measures Directional Alignment:** Determines how much two [[Vectors]] point in the same direction. 

- > Returns exactly `0` if they are perfectly perpendicular, a positive number if they point in the same general direction, and a negative number if they point in opposite directions.
    

#### 3D Graphics & Raytracing

##### Angle of Incidence 
[[Planes#Plane Intersection]] 
> Calculates the angle at which a ray strikes a surface by comparing the ray's direction vector against the surface's normal vector. Used to calculate glide paths and intersection distances.
    
##### Lighting Calculations (Lambertian Reflectance):
> Determines how bright a surface should be by taking the dot product of the incoming light direction and the surface normal. (Surfaces facing the light directly get maximum brightness; surfaces angled away get darker).
    
##### Backface Culling: 
> Determines if a polygon is facing toward or away from the camera. If the dot product between the camera's view vector and the polygon's normal is positive, the back of the polygon is facing the camera and can be skipped during rendering to save performance.
    

### Related
- [[std_iter_zip]]