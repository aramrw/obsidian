
#math #calculus #limits

by https://en.wikipedia.org/wiki/Isaac_Newton
https://en.wikipedia.org/wiki/Calculus

--- 

# Limits

## The Anatomy of a Limit

> A limit defines the behavior of an expression as a variable approaches a specific target value.

$$\lim_{h \to 0} \frac{f(x+h) - f(x)}{h}$$

## Component Definitions

- **Limit Operator ($\lim$):** Instructs the evaluation of a function's behavior near a point rather than exactly at that point.
- **Independent Variable ($h$):** The variable being varied. In the context of derivatives, this represents an infinitesimal *increment* or change ($\Delta x$).
- **Approach Condition ($\to$):** Indicates the direction of the variable's movement toward a target.
- **Target Value ($0$):** The specific coordinate or boundary value that the independent variable is approaching.
- **Argument / Expression ($\frac{f(x+h)-f(x)}{h}$):** The function or algebraic expression being evaluated by the limit operator. When defining a derivative, this specific fraction is called the *[[Difference Quotient]]*.

### The Special Limit

The special limit referred to is a fundamental geometric limit in calculus:

$$lim _{x\to 0}\frac{\sin (x)}{x}=1$$

When the angle $x$ is measured in radians and approaches 0, the value of $\sin(x)$ becomes almost exactly equal to $x$ itself.

## Graphs 

### Practice

![[Pasted image 20260608060008.png|420]]

To determine $\lim_{x \to 5} g(x)$, observe the behavior of the graph as $x$ approaches $5$ from both directions:

- **From the left:** As you trace the curve from $x = 3$ and $x = 4$ toward $x = 5$, the line drops downward. The trajectory aims directly at the open circle. If you look across to the $y$-axis, the vertical position of that circle is $-2$.
    
- **From the right:** As you trace the curve from $x = 7$ and $x = 6$ moving backward toward $x = 5$, the line also drops downward. This path aims at the exact same open circle at $y = -2$.
    

Because both the left and right paths converge on the same location—the hole at $(5, -2)$—the limit exists, and its value is $-2$.

The [[open circle]] indicates that the function itself is undefined at that exact moment; there is no solid ground there. However, a limit does not require the road to be whole to know where it is pointing. 

![[Pasted image 20260608060346.png|272]]

> Because the destination from the left ($-3$) is distinctly different from the destination from the right ($2$), the paths do not align. As established, a limit requires a single, unified destination from both directions. Since $-3 \neq 2$, the overall limit at $x = -4$ does not exist.

#### Limits of Combined Functions 

![[Pasted image 20260609122005.png|496]]

1. Find the limits of both graphs
2. Use the limit property to rewrite the problem
3. Plug and Solve

##### Piecewise 

![[Pasted image 20260609122651.png|491]]

1. Find the point as $x\to n^\pm$
2. Perform the operation on $f(x)$ and $g(x)$