#shaders #graphics #computer_graphics #computer_science #math #shader_tutorial

# Skybox Shader

A skybox is a method of creating backgrounds for 3D scenes. It involves drawing a cube around the camera and projecting an environment map (usually a [[Cubemap]]) onto it. 

This implementation renders a fullscreen [[Quad]] and [[Un-Project]]s its coordinates to find the correct 3D viewing direction, avoiding the need for an actual 3D [[Cube Mesh]]. 

It is built for `glslViewer` on macOS, which requires fallback to **GLSL 120** due to legacy OpenGL context limits.

## 1. Vertex Shader (Un-projecting the Quad)

Instead of rendering a 3D box, we draw a 2D [[Quad|screen-filling quad]]. We then use the inverse of the view-projection matrix to un-project these 2D screen coordinates into 3D world-space directions.

```glsl
#version 120
#ifdef GL_ES
precision highp float;
#endif

// Built-in uniforms for glslViewer
uniform mat4 u_viewMatrix; // See [[View Matrix]]
uniform mat4 u_projectionMatrix; // See [[Projection Matrix]]

// glslViewer provides this built-in attribute for the 2D quad
attribute vec4 a_position;

varying vec3 v_texCoord;

void main(void)
{
    // 1. Un-project the clip space coordinates to view space
    vec3 viewDir = vec3(
        a_position.x / u_projectionMatrix[0][0],
        a_position.y / u_projectionMatrix[1][1],
        -1.0
    );

    // 2. Compute the inverse of the view matrix
    // For a view matrix without scaling, the inverse of the rotation 
    // part is just its transpose.
    mat3 invView = mat3(
        u_viewMatrix[0][0], u_viewMatrix[1][0], u_viewMatrix[2][0],
        u_viewMatrix[0][1], u_viewMatrix[1][1], u_viewMatrix[2][1],
        u_viewMatrix[0][2], u_viewMatrix[1][2], u_viewMatrix[2][2]
    );

    // 3. Transform view direction to world direction
    // This direction vector becomes the 3D texture coordinate for the cubemap.
    v_texCoord = invView * viewDir;

    // 4. Set Depth
    // We set Z to 0.9999 so it renders extremely close to the far clipping plane (1.0).
    gl_Position = vec4(a_position.xy, 0.9999, 1.0);
}
```

## 2. Fragment Shader (Sampling the Cubemap)

The fragment shader takes the interpolated 3D direction vector (`v_texCoord`) and samples the `samplerCube` to get the final pixel color.

```glsl
#version 120
#ifdef GL_ES
precision highp float;
#endif

// The environment map loaded via command line arguments
uniform samplerCube u_cubeMap; 

varying vec3 v_texCoord;

void main(void)
{
    // Sample the cubemap using the 3D direction vector
    gl_FragColor = textureCube(u_cubeMap, v_texCoord);
}
```

## Run

```bash
glslViewer skybox.vert skybox.frag -c cubemap.png
```
