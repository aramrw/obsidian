#math #vector #geometry

# Magnitude (Vector Length)

In mathematics, the **magnitude** (or norm) of a vector is a scalar that represents its "length" or "size." It is the distance from the tail of the vector to its tip.

![[Pasted image 20260521011722.png]]
---

## 1. Notation
The magnitude of a vector $\mathbf{v}$ is usually denoted by double bars $\|\mathbf{v}\|$ or sometimes single bars $|\mathbf{v}|$.

---

## 2. The Formula (Euclidean Norm)
For a vector in 2D or 3D space, the magnitude is calculated using the Pythagorean theorem.

### 2D Vector
If $\mathbf{v} = (x, y)$:
$$\|\mathbf{v}\| = \sqrt{x^2 + y^2}$$

### 3D Vector
If $\mathbf{v} = (x, y, z)$:
$$\|\mathbf{v}\| = \sqrt{x^2 + y^2 + z^2}$$

### General N-Dimensional Vector
$$\|\mathbf{v}\| = \sqrt{\sum_{i=1}^{n} v_i^2}$$

---

## 3. Unit Vectors and Normalization
A **unit vector** is a vector with a magnitude of exactly $1$. 

**Normalization** is the process of taking any non-zero vector and scaling it so that its magnitude becomes $1$, while keeping its direction the same. This is done by dividing the vector by its own magnitude:
$$\mathbf{\hat{v}} = \frac{\mathbf{v}}{\|\mathbf{v}\|}$$

* **In Graphics:** Normalization is used constantly in [[GLSL Shaders]] to ensure light directions and surface normals are unit length for lighting calculations (like the Dot Product).

---

## 4. Relationship with Distance
The distance between two points $A$ and $B$ is simply the magnitude of the vector connecting them:
$$\text{dist}(A, B) = \|\mathbf{B} - \mathbf{A}\|$$

---

## 5. Programming Example (Rust)
If you have a vector struct, calculating magnitude looks like this:

```rust
struct Vec3 {
    x: f64,
    y: f64,
    z: f64,
}

impl Vec3 {
    pub fn magnitude(&self) -> f64 {
        (self.x.powi(2) + self.y.powi(2) + self.z.powi(2)).sqrt()
    }

    pub fn normalize(&self) -> Vec3 {
        let mag = self.magnitude();
        if mag == 0.0 { return Vec3 { x: 0.0, y: 0.0, z: 0.0 }; }
        Vec3 {
            x: self.x / mag,
            y: self.y / mag,
            z: self.z / mag,
        }
    }
}
```

---

## Related Concepts
* [[Euclidean]]
* [[Vectors]]
* [[Dot Product]]
* [[GLSL Shaders]]
* [[Simple Raytracing]]
