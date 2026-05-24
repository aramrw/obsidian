

<iframe width="520" height="320" frameborder="0" src="https://www.shadertoy.com/embed/l3XGDX?gui=true&t=10&paused=true&muted=false" allowfullscreen></iframe>

```glsl
#ifdef GL_ES
precision mediump float;
#endif

// GLSLViewer Uniforms
uniform vec2 u_resolution;
uniform float u_time;
uniform sampler2D u_tex0; // Replaces iChannel0 (Load your font texture here)

/* Heavily influenced by : 
   Necromurlok - https://www.shadertoy.com/view/ssf3zX 
   Xor - https://www.shadertoy.com/view/sd3czM - https://www.shadertoy.com/view/NdtyzM 
   Byte_mechanic - https://www.shadertoy.com/view/4fB3RR 
*/

uvec3 pcg3d(uvec3 p){
    p = p * 1234567u + 1234567890u;
    p.x *= p.y + p.z; p.y *= p.x + p.z; p.z *= p.y + p.x;
    p ^= p >> 16;
    p.x *= p.y + p.z; p.y *= p.x + p.z; p.z *= p.y + p.x;
    return p;
}

vec3 pcg3df(vec3 p){
    return vec3(pcg3d(floatBitsToUint(p))) / float(0xFFFFFFFFu);
}

float char(vec2 uv, vec2 idx){
    idx = floor(idx) * 1. / 16. ;
    uv += idx;
    // texture() is standard in modern GLSL, texture2D() for older versions
    return texture(u_tex0, clamp(uv, 0. + idx, 1. / 16. + idx)).r; 
}

void main() {
    // Normalized pixel coordinates (from 0 to 1) using GLSLViewer uniforms
    vec2 uv = (gl_FragCoord.xy - .5 * u_resolution.xy) / u_resolution.y;
    
    uv *= 1. + step(8. / 16., abs(uv.y));
    uv *= 1. + step(6. / 16., abs(uv.y));
    uv *= 1. + step(2. / 16., abs(uv.y));
    
    vec3 noise = pcg3df(uv.xyy);
    vec3 col = vec3(0.);
    vec2 fuv = floor(uv * 16.);
    vec3 rnd = pcg3df(fuv.yyy);
    
    uv.x += u_time * (rnd.x - .5) * .5;
    fuv = floor(uv * 16.);
    rnd = pcg3df(.0 * floor(u_time + noise.x * .1 + rnd.z) + fuv.xyy + rnd);
    uv = mod(uv, 1. / 16.) - (1. / 256.);
    
    col += char(uv, vec2(rnd.xy * 32.));
    col *= rnd.xzz;
    
    if(fract(rnd.y + rnd.x + rnd.y + u_time * .1 + noise.z * .01) < .1) {
        col = (1. - col) * rnd.xzz;
    }
    col *= length(rnd);
    
    gl_FragColor = vec4(col, 1.0);
}

```