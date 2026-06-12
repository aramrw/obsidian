### Declaration
```glsl
float step(float edge, float x) {}
```

### Description

`step()` generates a step function by comparing `x` to `edge`. 

```rust
if x >= edge:
	1.0
else
	0.0
```

Conceptually the same as:

```rust
fn less_or_greater(edge: f32, x: f32) -> f32 {
	match x <= edge {
		true => 1.0,
		false => 0.0	
	}	
}
```

```glsl
float step(float edge, float x)  
vec2 step(vec2 edge, vec2 x)  
vec3 step(vec3 edge, vec3 x)  
vec4 step(vec4 edge, vec4 x)

vec2 step(float edge, vec2 x)  
vec3 step(float edge, vec3 x)  
vec4 step(float edge, vec4 x)
```

### Parameters

`edge` specifies the location of the edge of the step function.

`x` specify the value to be used to generate the step function.

