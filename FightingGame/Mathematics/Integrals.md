#math #calculus #integrals
## Definite Integrals

--- 

### Example Problems

![[Pasted image 20260528080609.png|322]]

$$\int_{0}^{2} (3x^2 - 4x + 5) \, dx$$

To solve this, we must rely on the [[Fundamental Theorem of Calculus]], which requires finding the [[antiderivative]] and evaluating it at the given boundaries.

### Step 1: Find the [[Antiderivative]]

We apply the [[Power Rule]] of integration, $\int x^n \, dx = \frac{x^{n+1}}{n+1}$, to each term of the integrand $f(x) = 3x^2 - 4x + 5$.

$$F(x) = \int (3x^2 - 4x + 5) \, dx = \frac{3x^3}{3} - \frac{4x^2}{2} + 5x = x^3 - 2x^2 + 5x$$

The constant of integration $C$ is omitted here, as it naturally cancels out during the subtraction phase of a definite integral.

### Step 2: Evaluate at the Upper Limit

We substitute the upper boundary, $x = 2$, into the antiderivative function $F(x)$:

$$F(2) = (2)^3 - 2(2)^2 + 5(2)$$

$$F(2) = 8 - 8 + 10 = 10$$

### Step 3: Evaluate at the Lower Limit

We substitute the lower boundary, $x = 0$, into the antiderivative function $F(x)$:

$$F(0) = (0)^3 - 2(0)^2 + 5(0) = 0$$

### Step 4: Compute the Final Difference

According to the theorem, the value of the definite integral is the difference between the evaluation at the upper and lower limits:

$$\int_{0}^{2} (3x^2 - 4x + 5) \, dx = F(2) - F(0)$$

$$10 - 0 = 10$$

The definitive value of this integral is $10$.

### An Alternative Perspective

The accompanying plot displays this calculation as a shaded geometric area under the curve from $x = 0$ to $x = 2$. While the geometric interpretation of area is the most common way to visualize an integral, it is useful to view it from another perspective: net accumulation.

If $f(x)$ represented the fluctuating rate at which water flows into a reservoir over a period of two hours, the value of $10$ represents the total, objective volume of water accumulated during that time. The geometry is merely a tool for visualization; the calculation itself represents the absolute tracking of continuous change.