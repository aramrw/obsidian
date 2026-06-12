#matrix #math #computer_graphics #shaders 

# OpenGL 1.2

```glsl
#version 120

uniform mat4 u_modelViewProjectionMatrix;
uniform mat3 u_normalMatrix;

// (x,y,z,w) of the specific vertex
attribute vec4 a_position;
// The vector pointing straight out from the vertex, 
// used for calculating light bounces.
attribute vec3 a_normal;

varying vec3 v_localPos;
varying vec3 v_normal;

void main() {
  v_localPos = a_position.xyz;

  // Transform normal into view space
  v_normal = normalize(u_normalMatrix * a_normal);

  gl_Position = u_modelViewProjectionMatrix * a_position;
}

```

> Variables marked varying are the bridge between this vertex shader and the next stage of the pipeline: [[Fragment Shaders]].
> When a face is rendered, the GPU [[interpolates]] these varying values across the surface of the resulting triangle.