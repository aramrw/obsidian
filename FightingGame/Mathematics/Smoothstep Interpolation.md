#shaders #math

> https://en.wikipedia.org/wiki/Smoothstep

`smoothstep(edge0, edge1, x)` is a GLSL function that thresholds values, returning `0.0` or `1.0` while smoothly interpolating the boundary. 

It is the standard mechanism in #computer_graphics & #shaders for rendering crisp, anti-aliased geometry instead of hard, pixelated edges.

### Mathematics

```glsl
// Draws a smooth circle by interpolating between 0.4 and 0.41
float mask = smoothstep(0.4, 0.41, length(uv)); 
```

If we let $x = \text{length}(uv)$, the normalization formula is:

$$t = \frac{x - \text{edge}_0}{\text{edge}_1 - \text{edge}_0}$$

In the glsl code: 

$$t = \frac{x - 0.4}{0.41 - 0.4} = \frac{x - 0.4}{0.01}$$

Which simplifies to:

$$t = 100(x - 0.4)$$

$$t = 100x - 40$$

Now, `smoothstep` takes that $t$ value, clamps it between $0$ and $1$, and feeds it into the same $3t^2 - 2t^3$ cubic function we looked at earlier.

So, the exact piecewise mathematical formula for your specific `mask` variable looks like this:

$$\text{mask}(x) = \begin{cases} 0, & x \le 0.4 \\ 3(100x - 40)^2 - 2(100x - 40)^3, & 0.4 < x < 0.41 \\ 1, & x \ge 0.41 \end{cases}$$

Because your edges are so incredibly close together ($0.4$ and $0.41$), that middle cubic segment is very steep. Mathematically, it acts almost exactly like a standard linear step function, but that tiny $0.01$ window of cubic interpolation is what gives your circle a smooth, anti-aliased edge instead of a harsh, pixelated one.

![[Pasted image 20260525000646.png|365]]



![[Pasted image 20260524071806.png]]