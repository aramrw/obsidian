#computer_graphics #shaders #gamedev #textures

> https://en.wikipedia.org/wiki/UV_mapping

> UV mapping in computer graphics is a process for texture mapping a 3D model by projecting the model's surface coordinates onto a 2D image. 
> 
> The letters "U" and "V" denote the axes of the 2D texture because "X", "Y", and "Z" are already used to denote the axes of the 3D object in model space, while "W" (in addition to XYZ) is used in calculating [[Quaternions|Quaternian]] rotations, a common operation in computer graphics.

![[Pasted image 20260524122551.png|285]]

---
# Formula

UV coordinates on a sphere with Y-axis poles are determined by calculating the unit vector $\hat{d}$ from point $P$ to the origin, then applying specific formulas. 

The coordinates are calculated as $u = 0.5 + \frac{\operatorname{arctan2}(d_z, d_x)}{2\pi}$ and $v = 0.5 + \frac{\arcsin(d_y)}{\pi}$.

---
# Related 
- [[GLSL Shaders]]
- [[UV Normalization]]
