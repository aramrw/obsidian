#shaders #computer_graphics #math

A **Cubemap** is a specialized texture format consisting of six separate 2D square textures, each mapped to one face of a cube. In computer graphics, cubemaps are primarily used for environment mapping, [[Reflections]], and [[Skybox Shader|skyboxes]].

Unlike standard 2D textures that use `(u, v)` coordinates, a cubemap is sampled using a 3D direction vector `(x, y, z)`. The GPU determines which of the six faces the vector intersects and samples the texel at that location.

## Usage in Shaders
In GLSL, cubemaps are sampled using the `samplerCube` uniform type and the `texture()` or `textureCube()` function (depending on GLSL version). 

```glsl
uniform samplerCube u_cubeMap;
varying vec3 v_texCoord; // 3D direction vector

void main() {
    gl_FragColor = textureCube(u_cubeMap, v_texCoord);
}
```

## References
- [Wikipedia: Cube mapping](https://en.wikipedia.org/wiki/Cube_mapping)
- Linked to: [[Skybox Shader]], [[Cube Mesh]]
