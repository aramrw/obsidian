#math #computer_graphics #matrices

# View Matrix

The **View Matrix** is an affine transformation matrix that maps 3D world-space coordinates into view-space (or camera-space) coordinates. 

In a 3D engine, the camera does not actually move. Instead, the view matrix translates and rotates the *entire world* in the opposite direction of the camera's perceived position and orientation. 

## Structure
If the camera is at position $P$ with a rotation $R$, the View Matrix $V$ is mathematically the inverse of the camera's transformation matrix $C$:
$$ V = C^{-1} $$

When performing [[Un-Project|Un-Projection]] (such as in a [[Skybox Shader]]), we need the inverse of the View Matrix. For a matrix that only contains rotation (no scaling or translation), the inverse is equal to its transpose:
$$ R^{-1} = R^{T} $$

## Coordinate Pipeline
1. Model Matrix (Local $\rightarrow$ World)
2. **View Matrix** (World $\rightarrow$ Camera/View)
3. [[Projection Matrix]] (Camera/View $\rightarrow$ Clip Space)

## References
- [Wikipedia: Camera matrix](https://en.wikipedia.org/wiki/Camera_matrix)
- Linked to: [[Matrices]], [[Affine Transformations]], [[Projection Matrix]]
