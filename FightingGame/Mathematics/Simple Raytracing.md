### The Equation

$$P = O + tD$$

- $P$ is the **position** along the ray (the 3D hit point).
    
- $O$ is the ray's **origin** (the camera/eye position).
    
- $t$ is the distance **traveled** (a scalar value).
    
- $D$ is the **direction** the ray is pointing (a normalized vector).
    

> **Task:** Create a nested loop that iterates through every $X$ and $Y$ pixel of a Macroquad `Image`. For each pixel, calculate a ray shooting into the Z-axis (into the screen).

### Phase 3: Hitting a Sphere (The Silhouette)

Now you need an object to draw. A sphere is mathematically the easiest 3D shape to calculate because its intersection reduces to a quadratic equation.

- **The Math to Learn:** **Analytic Ray-Sphere Intersection**. Instead of stepping through space incrementally (which is _Raymarching_), you solve for $t$ algebraically to find the exact intersection instantly.
    
- **The Optimization:** In a standard quadratic equation ($t = \frac{-b \pm \sqrt{b^2 - 4ac}}{2a}$), $a = 1$ when the ray direction vector $D$ is normalized. Furthermore, the geometric definition of $b$ contains a factor of 2 ($b = 2b'$). By substituting these into the equation, the constants cancel out completely, leaving a highly optimized formula for the shader:
    
    $$t = -b' \pm \sqrt{(b')^2 - c}$$
    
    Where:
    
    - $\vec{V} = O - \text{SphereCenter}$ (vector from sphere center to ray origin)
        
    - $b' = \vec{D} \cdot \vec{V}$ (dot product of ray direction and $\vec{V}$)
        
    - $c = (\vec{V} \cdot \vec{V}) - \text{Radius}^2$
        
- **The Programming Task:** Write a function using this optimized equation. If the [[Discriminant]] under the radical ($(b')^2 - c$) is negative, the ray misses (color the pixel black). If it is positive, calculate the smallest positive value of $t$ to find the closest hit point, and color the pixel white.
    
- **The Drawing Connection:** You now have a flat, 2-dimensional silhouette. This demonstrates how 3D forms take up 2D space on a canvas (the concept of blocking out major shapes).
    

### Phase 4: Calculating the Normal (The Geometry of Form)

To shade the sphere, you need to know exactly which way the surface is curving at the exact microscopic point your ray hit it.

- **The Math to Learn:** Vector subtraction and normalization. For a sphere, the surface normal $\vec{N}$ is calculated by subtracting the sphere's center point from the exact hit position $P$ found in Phase 3, then dividing by the radius to normalize it.
    
- **The Programming Task:** Calculate the normal vector at the point of intersection:
    
    $$\vec{N} = \frac{P - \text{SphereCenter}}{\text{Radius}}$$
    
    Map the $X, Y, Z$ components of the normal vector to $R, G, B$ color channels to visualize the orientation of the surface.
    
- **The Drawing Connection:** This maps perfectly to visualizing **cross-contour lines**. Understanding the normal means understanding the volume, curvature, and underlying topography of the shape you are sketching.
    

### Phase 5: The Illumination (The Magic)

This is where the shadow mapping for your drawing practice comes to life.

- **The Math to Learn:** The Dot Product ($\vec{N} \cdot \vec{L}$) and Lambertian Reflectance.
    
- **The Programming Task:** Define a light source position (another `Vec3`). Calculate the normalized light direction vector $\vec{L}$ from the hit point $P$ toward the light. Take the dot product of the surface normal $\vec{N}$ and the light direction $\vec{L}$. Multiply your sphere's base color by this value:
    
    $$\text{Intensity} = \max(0.0, \vec{N} \cdot \vec{L})$$
    
- **The Drawing Connection:** You will immediately see the **terminator line** form where $\vec{N} \cdot \vec{L} = 0$. This visualizes exactly how the core shadow wraps around a form where light can no longer physically reach the surface.
    

### Phase 6: Interactive Study (Macroquad Integration)

- **The Programming Task:** Tie keyboard or mouse inputs in Macroquad to dynamically alter the light source's $X, Y, Z$ coordinates in real-time.
    
- **The Drawing Connection:** You now have a custom digital value study tool. You can move the light around and analyze exactly how the terminator line shifts, how form shadows compress near the edges, and where the brightest highlight lands relative to the light source vector.