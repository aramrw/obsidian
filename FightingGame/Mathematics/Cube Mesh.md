#computer_graphics #geometry

# Cube Mesh

A **Cube Mesh** is a standard 3D primitive geometry consisting of 8 vertices, 12 edges, and 6 square faces (rendered as 12 triangles). 

Historically, rendering a background environment involved placing the camera inside a massive Cube Mesh textured with a [[Cubemap]]. Today, it is mathematically faster to draw a single fullscreen 2D [[Quad]] and use [[Un-Project|Un-Projection]] to sample the cubemap per-pixel, skipping the 3D vertex transformations entirely.

## References
- [Wikipedia: Polygon mesh](https://en.wikipedia.org/wiki/Polygon_mesh)
- Linked to: [[Skybox Shader]], [[Cubemap]]
