### The Equation 
$P=O+tD$

- $P$ is the **position** along the ray.
- $O$ is the ray's **origin** (the camera).
- $t$ is the distance **traveled**.
- $D$ is the **direction** the ray is pointing.

> Create a loop that iterates through every $X$ and $Y$ pixel of a Macroquad `Image`. For each pixel, calculate a ray shooting into the Z-axis (into the screen).

### Phase 3: Hitting a Sphere (The Silhouette)

Now you need an object to draw. A sphere is mathematically the easiest 3D shape to calculate.

- **The Math to Learn:** The [[Quadratic Equation]] and [[Sphere Intersection]]. You are basically asking the math: "Does my ray line ever intersect with the radius of a sphere at coordinate $X, Y, Z$?"
    
- **The Programming Task:** Write a function that checks if a ray hits a sphere. If it hits, color that pixel white. If it misses, color it black.
    
- **The Drawing Connection:** You now have a flat, 2D silhouette. This teaches you how 3D forms take up 2D space on a canvas.
    

### Phase 4: Calculating the Normal (The Geometry of Form)

To shade the sphere, you need to know exactly which way the sphere is curving at the exact microscopic point your ray hit it.

- **The Math to Learn:** Vector subtraction for surface normals. For a sphere, the normal is just the hit position minus the sphere's center point.
    
- **The Programming Task:** Calculate the normal vector at the point of intersection. Map the $X, Y, Z$ of the normal to $R, G, B$ colors to visualize them.
    
- **The Drawing Connection:** This helps you visualize cross-contour lines. Understanding the normal means understanding the volume and topography of the shape you are sketching.
    

### Phase 5: The Illumination (The Magic)

This is where the shadow mapping for your drawing practice comes to life.

- **The Math to Learn:** The Dot Product ($\vec{N} \cdot \vec{L}$) and Lambertian Reflectance.
    
- **The Programming Task:** Define a light source position (another `Vec3`). Calculate the direction from the hit point to the light. Take the dot product of the surface normal and the light direction. Multiply your sphere's base color by this value.
    
- **The Drawing Connection:** You will immediately see the **terminator line** form. You will see how the core shadow wraps around the form where the light stops reaching.
    

### Phase 6: Interactive Study (Macroquad Integration)

- **The Programming Task:** Tie keyboard or mouse inputs in Macroquad to the light source's $X, Y, Z$ coordinates.
    
- **The Drawing Connection:** You now have a custom sandbox. You can move the light around and study exactly how the terminator line shifts, how the gradients compress near the edges, and where the brightest highlight lands.

