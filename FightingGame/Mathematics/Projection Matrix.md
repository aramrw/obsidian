#math #computer_graphics #matrices

# Projection Matrix

The **Projection Matrix** transforms 3D view-space (camera-space) coordinates into 2D clip-space coordinates. It defines the viewing volume (the frustum) of the camera and is responsible for perspective distortion (where objects further away appear smaller).

## Types of Projection
1. **Perspective Projection:** Simulates human vision. It divides the $X$ and $Y$ coordinates by the depth ($Z$) coordinate, causing distant objects to shrink.
2. **Orthographic Projection:** Maintains parallel lines. Objects remain the same size regardless of distance. Used in 2D games, UI rendering, and CAD software.

## Matrix Math
In an OpenGL perspective matrix, the diagonal elements `[0][0]` and `[1][1]` represent the scaling factors derived from the Field of View (FOV) and Aspect Ratio. 

During [[Un-Project|Un-Projection]], you can divide a coordinate by these diagonal elements to reverse the perspective projection and reconstruct the view-space vector.

## References
- [Wikipedia: 3D projection](https://en.wikipedia.org/wiki/3D_projection)
- Linked to: [[Matrices]], [[View Matrix]], [[Affine Transformations]]
