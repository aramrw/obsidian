#shaders #graphics #computer_graphics #computer_science #math #shader_tutorial

![[output 1.gif|254]]

```glsl
#ifdef GL_ES
precision mediump float;
#endif

uniform vec2 u_resolution;
uniform float u_time;

void main() {
    // 1. Center the universe 
    // so (0,0) is exactly in the middle of the canvas
    vec2 uv = (gl_FragCoord.xy * 1.95 - u_resolution.xy) / min(u_resolution.x, u_resolution.y);
    
    float t = u_time * 3. + 500. + sin(u_time / 3.) * 5.;
    
    // 2. Calculate from the physical center of the screen
    float dist = distance(uv, vec2(0., 0.)) * .4;
    float maxDist = .8;
    vec4 color;

    float expDist = dist * dist * dist;
    // Radial strength
    float strength = (sin(expDist * (0.04 * u_time)) + 1.) / 2.;
    float height = (sin(t * strength) + 1.) / 2.;
    float alpha = 1. - expDist / (maxDist * maxDist * maxDist) + (1. - height) * -0.014;
    
    color = vec4(.9, .9, .9, 1.) * height - (1. - alpha) * 0.652; 
    color.a = alpha;
    
    if(dist > maxDist) color = vec4(.1, .1, .1, 0.);
    
    // 3. Output directly to the standard GLSL fragment color
    gl_FragColor = color;
}

```