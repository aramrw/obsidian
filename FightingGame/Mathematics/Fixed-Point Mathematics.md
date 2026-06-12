#math #physics #networking

# Fixed-Point Mathematics

**Fixed-Point Mathematics** is a method of representing and calculating fractional numbers using integers, rather than using floating-point numbers (`float` or `double`). 

A fixed-point number designates a specific, unchanging number of bits to represent the integer part (whole number) and a specific number of bits to represent the fractional part.

## The Floating-Point Problem
In standard programming, `float` uses the IEEE 754 standard. Floating-point math is not completely deterministic across different CPU architectures or compiler optimizations. The operation `0.1 + 0.2` might yield `0.30000000000000004` on one machine and slightly differently on another. 

In fighting games using Rollback Netcode, both players' machines must simulate the exact same game state. If Player A's machine calculates a hitbox is at `10.51` and Player B's calculates `10.50`, Player A might register a hit while Player B registers a miss. The game desyncs.

## How Fixed-Point Works

Instead of the decimal point "floating", it is fixed. 

Let's simulate a simple decimal fixed-point system with 2 decimal places:
To represent `3.14`, you multiply it by $10^2$ ($100$) and store it as the integer `314`.
When you need to add `3.14` and `1.20`, you are actually doing integer math: `314 + 120 = 434`.

In actual computers, we use powers of 2 (bit shifting).
For a 32-bit integer, you might use **Q16.16 format**:
- 16 bits for the whole number.
- 16 bits for the fraction.

To convert a float to a Q16.16 fixed-point integer, you multiply by $2^{16}$ ($65536$):
`float f = 1.5;`
`int fixed = (int)(f * 65536.0); // Stores 98304`

## Arithmetic Operations
- **Addition/Subtraction:** Straightforward integer addition `(A + B)`.
- **Multiplication/Division:** Requires bit-shifting after the operation to adjust the fixed decimal place, because multiplying two Q16.16 numbers results in a Q32.32 number.

```c
// Example of fixed-point multiplication
int fixed_mul(int a, int b) {
    // Cast to 64-bit to prevent overflow during the multiplication,
    // then shift right by 16 bits to restore the Q16.16 scale.
    return (int)(((long long)a * (long long)b) >> 16);
}
```

## Application in Game Dev
- **Fighting Games & RTS:** Ensuring perfectly deterministic physics, [[Collision Detection]], and game logic for cross-platform network play.
- **Retro Emulation:** Older consoles (like the PS1 or GBA) did not have floating-point units (FPU); they relied entirely on fixed-point math.
