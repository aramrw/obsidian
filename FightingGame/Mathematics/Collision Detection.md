#math #physics #gamedev

Collision detection is the computational problem of detecting the intersection of two or more objects. In fighting games, this is primarily used for **Hitboxes** and **Hurtboxes**.

---

## 1. AABB vs AABB (Axis-Aligned Bounding Boxes)

This is the fastest and most common type of collision. It assumes the boxes are not rotated.

### The Logic
Two AABBs intersect if they overlap on **all** axes.

```rust
pub struct Rect {
    pub x: f32,
    pub y: f32,
    pub width: f32,
    pub height: f32,
}

impl Rect {
    pub fn intersects(&self, other: &Rect) -> bool {
        self.x < other.x + other.width &&
        self.x + self.width > other.x &&
        self.y < other.y + other.height &&
        self.y + self.height > other.y
    }
}
```

---

## 2. Circle vs Circle Collision

Ideal for projectiles or rounded characters.

### The Logic
Two circles collide if the distance between their centers is less than the sum of their radii.

$$\text{distance}(C_1, C_2) < R_1 + R_2$$

To optimize, we compare the **squared distance** to avoid a slow square root ($[[Euclidean]]$) calculation:

$$(x_2 - x_1)^2 + (y_2 - y_1)^2 < (R_1 + R_2)^2$$

```rust
pub fn circle_collision(p1: Vec2, r1: f32, p2: Vec2, r2: f32) -> bool {
    let dx = p1.x - p2.x;
    let dy = p1.y - p2.y;
    let distance_sq = dx * dx + dy * dy;
    let radius_sum = r1 + r2;
    
    distance_sq < radius_sum * radius_sum
}
```

---

## 3. Point in Rectangle (SDFs)

In shaders, we often use Signed Distance Functions (SDFs) to determine if a pixel is inside a shape.

### GLSL Implementation
```glsl
float rectSDF(vec2 p, vec2 b) {
    vec2 d = abs(p) - b;
    return length(max(d, 0.0)) + min(max(d.x, d.y), 0.0);
}

void main() {
    vec2 uv = gl_FragCoord.xy / u_resolution;
    float dist = rectSDF(uv - 0.5, vec2(0.2, 0.1));
    
    // If dist < 0, the pixel is inside the hitbox
    vec3 color = (dist < 0.0) ? vec3(1.0, 0.0, 0.0) : vec3(0.1);
    gl_FragColor = vec4(color, 1.0);
}
```

---

## 4. Advanced Concepts
* **OBB (Oriented Bounding Boxes):** Bounding boxes that can rotate. Requires the **Separating Axis Theorem (SAT)**.
* **Swept Volumes:** Calculating collision for fast-moving objects to prevent "tunneling" (passing through objects between frames).
* [[Minimum Bounding Box]]
* [[Euclidean]] (Distance calculations)
