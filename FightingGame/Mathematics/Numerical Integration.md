#math #physics

# Numerical Integration

**Numerical Integration** in the context of game physics is the method used to approximate the position and velocity of objects over time, updating them step-by-step in discrete frames. 

Because we cannot calculate the exact continuous path of a physics object instantaneously, we slice time into tiny chunks (Delta Time) and calculate the change in state.

## The Core Concept
From [[Vector Calculus]], we know:
1. **Position** changes based on **Velocity**.
2. **Velocity** changes based on **Acceleration** (Force / Mass).

Integration is the process of taking acceleration, calculating the new velocity, and then using that velocity to calculate the new position for the current frame.

## Common Integrators

### 1. Explicit Euler Integration (The Simplest)
This is what most beginners write intuitively. It uses the *current* velocity to update position, then updates the velocity.

```rust
// Euler Integration
position = position + velocity * delta_time;
velocity = velocity + acceleration * delta_time;
```
* **Pros:** Very simple, extremely fast.
* **Cons:** Highly inaccurate. Errors accumulate quickly, causing systems (like orbital mechanics or springs) to gain energy and explode over time.

### 2. Semi-Implicit Euler (Symplectic Euler)
The standard for basic game physics. You update velocity *first*, and then use that *new* velocity to update the position.

```rust
// Semi-Implicit Euler
velocity = velocity + acceleration * delta_time;
position = position + velocity * delta_time; // Uses the updated velocity
```
* **Pros:** Still very simple, but significantly more stable. It conserves energy much better over time.
* **Cons:** Still not accurate enough for rigid complex simulations.

### 3. Verlet Integration
Instead of storing velocity, Verlet integration stores the *current position* and the *previous position*. It infers the velocity based on how far the object moved last frame.

```rust
// Verlet Integration
let temp = position;
position = position + (position - previous_position) + (acceleration * delta_time * delta_time);
previous_position = temp;
```
* **Pros:** Incredibly stable for constraints. Heavily used in cloth simulations, ragdolls, and rope physics.
* **Cons:** Dealing with sudden velocity changes (like impulses or teleportation) can be tricky because velocity isn't explicitly stored.

### 4. Runge-Kutta 4 (RK4)
The gold standard for high-accuracy simulations. It samples the forces at multiple points throughout the timestep (beginning, middle, and end) and averages them out to calculate the final curve.
* **Pros:** Incredibly accurate. Used for space flight sims (Kerbal Space Program) and precise racing games.
* **Cons:** Computationally expensive (requires evaluating acceleration 4 times per object per frame). Usually overkill for action or fighting games.
