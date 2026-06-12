#shaders #computer_graphics #geometry #computer_science

# 3D Geometry Formats (.OBJ)

In computer graphics, a 3D model is essentially a text file containing lists of mathematical coordinates that describe a shape. The **Wavefront .obj** file is one of the oldest, simplest, and most universally supported formats for storing this 3D geometry data.

While graphics programmers almost never write `.obj` files by hand (they are exported from software like Blender or Maya), understanding their structure is crucial because it directly mirrors how data is passed from the CPU to a [[GLSL Shaders|Shader]] on the GPU.

## The Anatomy of an OBJ File

A standard `.obj` file is broken down into three primary components: Vertices, Normals, and Faces.

### 1. Vertices (`v`)
```obj
v -0.5 -0.5  0.5
v  0.5 -0.5  0.5
```
The `v` stands for vertex. These are raw 3D coordinates $(X, Y, Z)$ defining points in local space. A standard [[Cube Mesh]] has 8 corners, so an OBJ of a cube will have 8 `v` lines. 

* **In Shaders:** This data is piped directly into vertex shader attributes, commonly named `attribute vec4 a_position` or `in vec3 position`.

### 2. Vertex Normals (`vn`)
```obj
vn  0.0  0.0  1.0
vn  0.0  0.0 -1.0
```
The `vn` stands for vertex normal. These are 3D direction vectors $(X, Y, Z)$ that dictate which way a surface is facing. They are mathematically normalized (their [[Magnitude]] is 1.0). Normals are fundamentally required for calculating lighting, shadows, and reflections. 

* **In Shaders:** This data is piped into `attribute vec3 a_normal`. It is often transformed by the [[View Matrix]] (or a dedicated normal matrix) to calculate light direction in view-space.

### 3. Faces / Indices (`f`)
```obj
f 1//1 2//1 4//1 3//1
```
The `f` stands for face. This is the "connect the dots" instruction set. It tells the graphics pipeline how to connect the raw vertices (`v`) together to form polygons (usually triangles or [[Quadrilateral|Quads]]). 

The format is typically `vertex_index / texture_coordinate_index / normal_index`. 
*(Note: If a mesh doesn't have texture coordinates, it leaves that space blank, resulting in `//`)*.

For example, `f 1//1 2//1 4//1 3//1` translates to:
> "Draw a polygon connecting Vertex #1, Vertex #2, Vertex #4, and Vertex #3, and ensure all of them use Normal #1."

* **In the Graphics Pipeline:** This data isn't processed by the shader directly. Instead, the CPU uses these indices to know *which* vertices to grab from memory and feed into the vertex shader.

# FlatPlane

![[Pasted image 20260525014154.png|304]]

```obj
# Vertices (v x y z)
v -1.0 -1.0 0.0
v  1.0 -1.0 0.0
v  1.0  1.0 0.0
v -1.0  1.0 0.0

# Face (f v1 v2 v3 v4)
f 1 2 3 4

```

### 1. The Vertices (`v`)


![[Screenshot 2026-05-25 at 1.45.35 AM.png|383]]

Every line starting with `v` defines a single point in 3D space using standard Cartesian coordinates ($x$, $y$, $z$).

- `v -1.0 -1.0 0.0`: 
	- $x = -1$, $y = -1$. 
	- This is the **bottom-left** corner.
    
- `v 1.0 -1.0 0.0`: 
	- $x = 1$, $y = -1$. 
	- This is the **bottom-right** corner.
    
- `v 1.0 1.0 0.0`: 
	- $x = 1$, $y = 1$.
	- This is the **top-right** corner.
    
- `v -1.0 1.0 0.0`: 
	- $x = -1$, $y = 1$. 
	- This is the **top-left** corner.
    

Because every single $z$-value is `0.0`, these points have no depth. They lie perfectly flat along the XY plane.

### 2. The Face (`f`)

Vertices floating in space are invisible in a 3D render until you connect them. The line starting with `f` defines a solid surface (a polygon) by linking the vertices together.

- `f 1 2 3 4` translates to: "Create a surface by connecting vertex 1 to vertex 2, then to 3, then to 4, and close the loop back to 1."
    
- **Important Note:** The `.obj` format uses **1-based indexing**. The first vertex you define in the file is index `1`, not `0` (which is a common trip-up if you are writing a custom parser in a language like Rust, where arrays are 0-indexed).
    

### Why This Specific Shape Matters

This exact 4-vertex, 1-face structure—a completely flat quad resting at $z=0$—is incredibly useful in rendering pipelines. When constructing 2D-in-3D assets for retro-style engines, this planar mesh is the "billboard." The engine takes a sprite texture (like a monster or a tree), maps it onto this exact square, and then uses linear algebra transformation matrices in the vertex shader to rotate the quad so it always faces the player's camera.

## Summary

You do not need to memorize OBJ syntax. However, the core conceptual workflow—loading arrays of **Positions**, **Normals**, and **Texture Coordinates (UVs)**, and stitching them together using **Indices**—is the foundational mechanism of all 3D rendering APIs, including OpenGL, Vulkan, Direct3D, and Metal.

## References
- [Wikipedia: Wavefront .obj file](https://en.wikipedia.org/wiki/Wavefront_.obj_file)
- Linked to: [[Cube Mesh]], [[GLSL Shaders]], [[View Matrix]]