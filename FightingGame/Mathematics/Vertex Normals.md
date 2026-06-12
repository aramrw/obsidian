### .OBJ (`vn`)

```obj
vn  0.0  0.0  1.0
vn  0.0  0.0 -1.0
```

The `vn` stands for vertex normal. These are 3D direction vectors  that dictate which way a surface is facing. They are mathematically normalized (their [[Magnitude]] is 1.0). Normals are fundamentally required for calculating lighting, shadows, and reflections.

- It is often transformed by the [[View Matrix]](or a dedicated normal matrix) to calculate light direction in view-space.
- **In Shaders:** This data is piped into `attribute vec3 a_normal`. 

```glsl 
#version 120

uniform mat4 u_modelViewProjectionMatrix;
uniform mat3 u_normalMatrix;

// (x,y,z,w) of the specific vertex
attribute vec4 a_position;
// The vector pointing straight out from the vertex, 
// used for calculating light bounces.
attribute vec3 a_normal;
```