#shaders #math #computer_graphics #linear_algebra #calculus #discrete_math 
# Simplex Noise

[Source: Wikipedia](https://en.wikipedia.org/wiki/Simplex_noise)

Simplex Noise is a method for generating smooth, continuous procedural noise. It is often used as a more computationally efficient and artifact-free alternative to Perlin Noise.

In shader programming and computer graphics, Simplex Noise is frequently used for [[Domain Warping]] to distort coordinates smoothly without introducing mathematical [[asymptotes]].

---

### Diagram

> See for more info: [[Simplex Noise#Squashing Squares]]

![[output.gif]]

---

**Simplex noise** is the result of an $n$-dimensional [gradient noise](https://en.wikipedia.org/wiki/Gradient_noise) function comparable to [Perlin noise](https://en.wikipedia.org/wiki/Perlin_noise) ("classic" noise) but with fewer [directional artifacts](https://en.wikipedia.org/wiki/Isotropy), in higher dimensions, and a lower computational overhead. [Ken Perlin](https://en.wikipedia.org/wiki/Ken_Perlin) designed the algorithm in 2001 to address the limitations of his classic noise function, especially in higher dimensions.

The advantages of simplex noise over Perlin noise:

- Simplex noise has lower computational complexity and requires fewer multiplications.
- Simplex noise scales to higher dimensions (4D, 5D) with much less computational cost: the complexity is $O(n^2)$ for $n$ dimensions instead of the $O(n\,2^{n})$ of classic noise.
- Simplex noise has no noticeable directional artifacts (is visually [isotropic](https://en.wikipedia.org/wiki/Isotropic)), though noise generated for different dimensions is visually distinct (e.g., 2D noise has a different look than 2D slices of 3D noise, and it looks increasingly worse for higher dimensions).
- Simplex noise has a well-defined and continuous gradient (almost) everywhere that can be computed quite cheaply.
- Simplex noise is easy to implement in hardware.

Whereas Perlin noise interpolates between the [[Gradient|Gradients]] at the surrounding hypergrid end points (i.e., northeast, northwest, southeast and southwest in 2D), simplex noise divides the space into [simplices](https://en.wikipedia.org/wiki/Simplex) (i.e., $n$-dimensional triangles). This reduces the number of data points. While a hypercube in $n$ dimensions has $2^n$ corners, a simplex in $n$ dimensions has only $n+1$ corners. The triangles are [equilateral](https://en.wikipedia.org/wiki/Equilateral_triangle) in 2D, but in higher dimensions the simplices are only approximately regular. For example, the tiling in the 3D case of the function is an orientation of the [tetragonal disphenoid honeycomb](https://en.wikipedia.org/wiki/Tetragonal_disphenoid_honeycomb).

Simplex noise is useful for computer graphics applications, where noise is usually computed over 2, 3, 4, or possibly 5 dimensions. For higher dimensions, $n$-spheres around $n$-simplex corners are not densely enough packed, reducing the support of the function and making it zero in large portions of space.

## Algorithm Detail

To understand what it is saying, we have to look at the central problem Simplex noise is trying to solve: **Computers are very fast at finding grids, but very slow at finding triangles.**

If you have a standard $(x, y)$ coordinate like: $(1.2, 3.7)$,

The computer instantly knows it is inside the grid square starting at $(1, 3)$. It just chops off the decimals (an operation called `floor`):

```rust
#[derive(Copy, Clone, Debug)]
struct Vec2 {
    x: f32,
    y: f32,
}
fn vec2(x: f32, y: f32) -> Vec2 {
  Vec2 { x, y }   
}

fn main() {
    let v = vec2(1.7, 3.1);
    let fv = vec2(v.x.floor(), v.y.floor());
    dbg!(fv);
}
```

```rust
[src/main.rs:14:5] fv = Vec2 {
    x: 1.0,
    y: 3.0,
}
```

### However

Simplex noise **doesn't use squares**.

Tt uses an interlocking web of triangles (a simplical grid): [Simplex](https://en.wikipedia.org/wiki/Simplex). 

There is no instant `floor` math to figure out which triangle a coordinate is floating inside. So, Ken Perlin (the inventor) used a clever trick: he squashed the grid, using #linear_algebra and [[Vectors and Matrices]].

Here is the breakdown of exactly what that math is doing in 2D space.

---

## Squashing Squares 

Imagine a regular grid of squares made out of flexible wire. If you grab the top-right corner of a square and the bottom-left corner, and pull them away from each other, the square squishes into a diamond (a rhombus).

If you pull it by _exactly_ the mathematical amount $F$, that diamond stretches until the line connecting its two closest corners becomes exactly the same length as its outer edges. You have just deformed a square into **two perfect equilateral triangles**. See: [[Simplex Noise#Diagram]]

This is what the text means by: _"until the distance between the points $(0,0,...,0)$ and $(1,1,...,1)$ becomes equal to the distance between the points $(0,0,...,0)$ and $(1,0,...,0)$"_.

### 2. The Skew Formula

> Stretches normal space into this squashed triangle space. Also known as [[Affine Transformations]].

$$x_i' = x_i + (x_1 + ... + x_n) \cdot F$$

In 2D (where $n = 2$), the skew factor $F$ simplifies to:

$$F = \frac{\sqrt{3} - 1}{2} \approx 0.366$$

If you want to evaluate the noise at a specific pixel $(x, y)$, you plug those coordinates into the formula. The math physically stretches the coordinate axis, mapping your normal screen pixel into this warped, diamond-shaped universe.

### 3. "Determine which skewed unit hypercube cell the input point lies in"

This is the punchline. Why did we do all of this squashing?

Because inside this warped universe, those diamonds mathematically behave exactly like squares again. To find out which diamond our point is inside, the computer can just chop off the decimals of our new skewed coordinates $(x', y')$.

$$x_b = \lfloor x' \rfloor$$

$$y_b = \lfloor y' \rfloor$$

Once the computer knows which diamond (cell) it is in, a single, incredibly cheap `if` statement tells it which of the two triangles it is in:

- If the fractional part of $x'$ is greater than the fractional part of $y'$, you are in the bottom triangle.
    
- Otherwise, you are in the top triangle.
    

The entire complicated formula is just a mathematical optical illusion to trick the computer into calculating triangles using fast, cheap square-grid logic.

