#math #shaders #rendering

# Barycentric Coordinates

**Barycentric Coordinates** are a coordinate system in which the location of a point is specified by reference to a simplex (a triangle in 2D space, a tetrahedron in 3D). 

In game development, they are most commonly used to define any point *inside* a triangle based on the "weight" or influence of the triangle's three vertices.

## Concept

If you have a triangle defined by three vertices ($V_1$, $V_2$, $V_3$), any point $P$ inside that triangle can be expressed as a mixture of those three vertices using three weights ($u$, $v$, $w$):

$$P = uV_1 + vV_2 + wV_3$$

For a point to be strictly *inside* the triangle, all three weights must be between 0.0 and 1.0, and they must sum up to exactly 1.0:
$$u + v + w = 1.0$$

> **Visualizing the weights:** If the point $P$ is exactly on vertex $V_1$, then $u=1$, $v=0$, and $w=0$. If $P$ is dead center in the middle of the triangle, $u$, $v$, and $w$ will all be $0.333$.

## Applications in Game Dev

1. **Interpolation (The core of rasterization):** When a GPU draws a triangle, the Vertex Shader calculates data (like color, [[UV Mapping|UV coordinates]], or [[Normals]]) for the three corners. The Fragment Shader then uses Barycentric Coordinates to smoothly [[Interpolation|interpolate]] those values across the pixels in the middle of the triangle.
2. **Terrain Placement:** If a character is walking on a sloped 3D mesh (navmesh), you use Barycentric Coordinates to calculate exactly how high (Y-axis) the character should be when standing at a specific (X, Z) coordinate on a specific triangle.
3. **Hit Location (Shooters):** Determining exactly where a bullet struck a target's mesh to apply the correct texture decal (bullet hole).

## Finding the Coordinates
If you know the positions of $V_1, V_2, V_3$ and the point $P$, you typically calculate the weights using areas of sub-triangles. The math relies heavily on the [[Cross Product]] to find the areas of the triangles formed by $P$ and the edges.
