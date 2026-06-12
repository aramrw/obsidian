#shaders #computer_graphics #geometry

![[Pasted image 20260525003533.png]]

# Quad (Screen-Filling Quad)

A **Quad** (short for quadrilateral) is a foundational 2D polygon with four vertices. 

In modern computer graphics, a **Screen-Filling Quad** (or fullscreen quad) is a 2D quad rendered such that it exactly covers the camera's viewport. Rather than rendering complex 3D geometry like a [[Cube Mesh]], graphics programmers often render a simple 2D quad and manipulate the coordinate space directly in the shader.

## Applications
- **Post-Processing:** Applying full-image effects (blur, bloom, color grading).
- **[[Skybox Shader]]:** By rendering a quad at the far clipping plane and using [[Un-Projection]], you can sample a [[Cubemap]] background without pushing 3D cube vertices through the graphics pipeline.
- **Raymarching/Raytracing:** A quad acts as the canvas upon which mathematical rays are cast into a mathematical scene.

## References
- [Wikipedia: Quadrilateral](https://en.wikipedia.org/wiki/Quadrilateral)
- Linked to: [[Quadrilateral]], [[Skybox Shader]]
