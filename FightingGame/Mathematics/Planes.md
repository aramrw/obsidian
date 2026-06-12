#math #trigonometry #linear_algebra #algebra 



# 2D Planes 

# 3D Planes 

![[Pasted image 20260525003944.png]]

> A plane in 3D space is defined by two things:

- `planeNormal`: A arrow pointing directly straight up, perpendicular to the flat surface.
- `planeDist`: How far the plane is shifted away from the center of the world `(0,0,0)`

---

### Plane Intersection
> BackLink: [[Dot Product#3D Graphics & Raytracing#Angle of Incidence]]

![[Pasted image 20260525004218.png]]

```glsl
// Returns distance to intersection, or -1.0 if miss
float intersectPlane(
	vec3 rayOrigin, 
	vec3 rayDir, 
	vec3 planeNormal, 
	float planeDist
) {
  float denominator = dot(rayDir, planeNormal);

  // Guard against parallel rays dividing by zero
  if (abs(denominator) > 0.001) {
    // get the dot product.
    float dotp = dot(RayOrigin, planeNormal);
    // this does something
    dotp += planeDist;
    // make it neg then num/denom
    float t = -(dotp) / denominator;
    if (t >= 0.0) return t;
  }
  return -1.0;
}
```

###### Denominator 
> Mathematically, `dot(rayDir, planeNormal)` calculates how closely the ray's direction matches the plane's normal. Usually these values are [[Magnitude|Normalized]]
> [[Dot Product]]

##### Algebraic Expansion (3D Space) Formula

$$\mathbf{d} \cdot \mathbf{n} = d_x n_x + d_y n_y + d_z n_z$$

##### Plane Intersection Mathematical Formulas

$$\mathbf{d} \cdot \mathbf{n} = \|\mathbf{d}\| \|\mathbf{n}\| \cos(\theta)$$

######  Breakdown

* **$\mathbf{d}$**: The ray direction vector.
* **$\mathbf{n}$**: The plane normal vector.
* **$\cdot$**: The dot product operator.
* **$\|\mathbf{d}\|$**: The length (magnitude) of the ray direction vector.
* **$\|\mathbf{n}\|$**: The length (magnitude) of the plane normal vector.
* **$\theta$**: The angle between the two vectors.

##### Simplified Unit Vector Notation

If both vectors are normalized, the equation simplifies to:

$$\mathbf{d} \cdot \mathbf{n} = \cos(\theta)$$


### Example Setup

**The Plane (The Ground):**
*   **Normal ($\mathbf{n}$)**: `vec3(0.0, 1.0, 0.0)` (Pointing straight up along the Y-axis)
*   **Distance ($d$)**: `0.0` (Sits perfectly at $Y = 0$)

**The Ray (The Camera):**
*   **Origin ($\mathbf{o}$)**: `vec3(0.0, 5.0, 0.0)` (Floating at $Y = 5$)
*   **Direction ($\mathbf{d}$)**: `vec3(1.0, 0.0, 0.0)` (Looking straight along the X-axis)

---

### Step 1: Denominator (Alignment)

$$\text{dot}(\mathbf{n}, \mathbf{d}) = (0.0 \times 1.0) + (1.0 \times 0.0) + (0.0 \times 0.0) = 0.0$$

*   **Result**: `0.0`
*   **Meaning**: The ray is perfectly parallel to the plane.

---

### Step 2: Numerator (Altitude)

$$\text{dot}(\mathbf{o}, \mathbf{n}) + d = (0.0 \times 0.0) + (5.0 \times 1.0) + (0.0 \times 0.0) + 0.0 = 5.0$$

*   **Result**: `5.0`

---

### Step 3: Final Division ($t$)

$$t = \frac{\text{Numerator}}{\text{Denominator}} = \frac{5.0}{0.0} \implies \text{Division by Zero!}$$

*   **Conclusion**: Because you are dividing by `0.0`, the ray will never intersect the plane. This mathematically confirms they run perfectly parallel to each other.

---

# Related
- [[Rays]]