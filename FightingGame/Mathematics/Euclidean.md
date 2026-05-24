#math #geometry #vectors

# Euclidean Space and Distance

In mathematics, **Euclidean** geometry and distance form the basis for most physics and spatial calculations in game development. It describes the "standard" 2D and 3D space we are familiar with.

---

## 1. Euclidean Distance
The **Euclidean distance** between two points is the length of the line segment connecting them. In a 2D or 3D coordinate system, this is calculated using the Pythagorean theorem.

### Formula (2D)
For points $P_1(x_1, y_1)$ and $P_2(x_2, y_2)$:
$$d = \sqrt{(x_2 - x_1)^2 + (y_2 - y_1)^2}$$

### Formula (3D)
For points $P_1(x_1, y_1, z_1)$ and $P_2(x_2, y_2, z_2)$:
$$d = \sqrt{(x_2 - x_1)^2 + (y_2 - y_1)^2 + (z_2 - z_1)^2}$$

---

## 2. Squared Euclidean Distance (Performance Tip)
Calculating the square root (`sqrt`) is computationally expensive. In many game development scenarios (like range checks or sorting by distance), you can use the **Squared Euclidean Distance** instead:

$$d^2 = (x_2 - x_1)^2 + (y_2 - y_1)^2$$

* **Example:** To check if an enemy is within range `R`, compare $d^2 < R^2$ instead of $d < R$.

---

## 3. Euclidean Norm
The **Euclidean Norm** (also known as the $L^2$ norm) is the [[Magnitude]] of a vector. It represents the distance from the origin $(0,0,0)$ to the point defined by the vector.

$$\|\mathbf{v}\|_2 = \sqrt{\sum_{i=1}^{n} v_i^2}$$

---

## 4. Euclidean Geometry in Fighting Games
* **Hitboxes:** Most circular or spherical hitboxes rely on Euclidean distance for collision detection.
* **Movement:** Calculating the shortest path between two fighters.
* **Proximity:** Determining when to trigger "close-range" vs "long-range" animations.

---

## Programming Example (Rust)
```rust
fn euclidean_distance(p1: (f64, f64), p2: (f64, f64)) -> f64 {
    let dx = p2.0 - p1.0;
    let dy = p2.1 - p1.1;
    (dx*dx + dy*dy).sqrt()
}

fn euclidean_distance_sq(p1: (f64, f64), p2: (f64, f64)) -> f64 {
    let dx = p2.0 - p1.0;
    let dy = p2.1 - p1.1;
    dx*dx + dy*dy
}
```

---

## Related Concepts
* [[Magnitude]]
* [[Heuristics]] (Euclidean Distance is a common heuristic)
* [[Distance Functions]] (Vertical vs. Euclidean)
* [[Vectors]]
* [[Complex Numbers]]
