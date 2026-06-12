#math #computer_graphics #shaders

# Un-Projection

**Un-Projection** (or inverse projection) is the mathematical process of transforming 2D screen or clip-space coordinates back into 3D view-space or world-space directions/positions. 

While rendering normally projects 3D vertices onto a 2D screen using a [[Projection Matrix]] and [[View Matrix]], *un-projection* runs this process in reverse. This is particularly useful for raycasting from the mouse cursor, or for rendering a [[Skybox Shader]] on a 2D [[Quad]].

## The Mathematics
To un-project a 2D screen coordinate, you typically:
1. Convert the screen pixel coordinate to Normalized Device Coordinates (NDC) ranging from -1.0 to 1.0.
2. Multiply by the **inverse** of the [[Projection Matrix]] to get the view-space ray direction.
3. Multiply by the **inverse** of the [[View Matrix]] to transform that ray into world-space.

```glsl
// Un-projecting in a Skybox vertex shader
vec3 viewDir = vec3(
    a_position.x / u_projectionMatrix[0][0],
    a_position.y / u_projectionMatrix[1][1],
    -1.0
);
```

## References
- [Wikipedia: 3D projection](https://en.wikipedia.org/wiki/3D_projection)
- Linked to: [[Matrices]], [[Projection Matrix]], [[View Matrix]]
