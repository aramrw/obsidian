#math #computer_graphics #geometry #raytracing #shaders 

> In computer graphics, physics simulations, and mathematics, a [[Rays|Ray]] is represented as a semi-infinite line that has a specific starting point and propagates infinitely in one direction.

# Formula

> A ray is commonly expressed using a vector equation: 

$$
P(t)=rayOrigin+t(rayDirection)
$$

## Component Breakdown

- $\text{rayOrigin}$: A 3D point $(x, y, z)$ marking the starting position.
- $\text{rayDir}$: A 3D vector $(x, y, z)$ representing the direction. 
	- It is usually [[Magnitude|normalized]] to simplify calculations.
- $t$: A scalar parameter representing distance. For a valid ray, $t$ must be greater than or equal to zero ($t \ge 0$). To prevent the laser from shooting backward, code libraries simply ignore any intersection where $t$ is negative.


## Common Use Cases

- Ray Tracing: Simulating light bouncing off objects to create realistic rendering.
- [[Collision Detection]]: Checking if a bullet or laser hits a target in video games.
- Mouse Picking: Determining which 3D object a user clicked on a 2D screen. 

# Related
- [[Planes]]

