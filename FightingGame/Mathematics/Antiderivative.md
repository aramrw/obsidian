#math #calculus 

https://en.wikipedia.org/wiki/Antiderivative

> In [calculus](https://en.wikipedia.org/wiki/Calculus "Calculus"), an **antiderivative**, **inverse derivative**, **primitive function**, **primitive integral** or **indefinite integral** of a [function](https://en.wikipedia.org/wiki/Function_\(mathematics\) "Function (mathematics)") _f_ is a [differentiable function](https://en.wikipedia.org/wiki/Differentiable_function "Differentiable function") _F_ whose [derivative](https://en.wikipedia.org/wiki/Derivative "Derivative") is equal to the original function _f_. This can be stated symbolically as _F'_ = _f_.[[1]](https://en.wikipedia.org/wiki/Antiderivative#cite_note-2)[[2]](https://en.wikipedia.org/wiki/Antiderivative#cite_note-3) The process of solving for antiderivatives is called **antidifferentiation** (or **indefinite integration**), and its opposite operation is called _differentiation_, which is the process of finding a derivative. Antiderivatives are often denoted by capital [Roman letters](https://en.wikipedia.org/wiki/Roman_letters "Roman letters") such as F and G.

--- 

## Examples

Understanding the mechanics of integration requires stepping back from the final calculation and examining the inverse operations that make it possible.

The process rests entirely on **differentiation** and **integration**. To understand how to solve the definite integral problem, you must first master the **Antiderivative**.

## 1. What is an Antiderivative?

An antiderivative is simply the reverse process of finding a [[Derivative]].

- **Differentiation:** You start with a function and find its rate of change (the derivative).
    
- **Antidifferentiation:** You start with a rate of change and find the original function.
    

If you are given a function $f(x) = 2x$, the antiderivative asks: _"What function did we differentiate to get $2x$?"_ Knowing the basic [[Power Rule]]s of [[Derivative#2. The Power Rule for Derivatives]], the answer is $x^2$, because the derivative of $x^2$ is $2x$:

$$x^2 = (2 \times 1)(x^{2-1}) = 2x$$

### The Constant of Integration ($C$)

When you differentiate a constant number (like $5$, $-10$, or $\pi$), the result is always $0$ because a constant does not change.

- The derivative of $x^2 + 5$ is $2x$.
    
- The derivative of $x^2 - 100$ is also $2x$.
    

Because we lose the specific constant during differentiation, we must add a generic constant, written as $+ C$, to the end of every indefinite integral.

$$\int 2x \, dx = x^2 + C$$

## 2. The Power Rule for Integration

To solve polynomials (expressions with variables raised to exponents, like $x^2$ or $x^3$), we use the **Power Rule**. This is the exact opposite of the power rule used in derivatives.

Instead of multiplying by the exponent and subtracting one, you do the reverse operations in reverse order:

1. **Add 1** to the exponent.
    
2. **Divide** by this new exponent.
    

### The General Formula:

$$\int x^n \, dx = \frac{x^{n+1}}{n+1} + C$$

_(This rule applies to any exponent where $n \neq -1$.)_

## 3. Step-by-Step Example Problems

Here are three examples, moving from a single basic term to the multi-term expression used in the previous definite integral problem.

### Example 1: A Single Power Term

Find the antiderivative of $x^2$.

- **Step 1:** Identify the exponent, which is $n = 2$.
    
- **Step 2:** Add $1$ to the exponent: $2 + 1 = 3$.
    
- **Step 3:** Divide the term by this new exponent: $\frac{x^3}{3}$.
    
- **Step 4:** Add the constant $C$.
    

$$\int x^2 \, dx = \frac{x^3}{3} + C$$

### Example 2: Handling Coefficients (Numbers in Front)

Find the antiderivative of $3x^2$.

When a variable has a constant multiplier (a coefficient) in front of it, the multiplier remains unchanged during the integration process. You simply integrate the variable part and then multiply.

- **Step 1:** Leave the $3$ alone for a moment and focus on $x^2$.
    
- **Step 2:** Apply the power rule to $x^2$, which gives $\frac{x^3}{3}$ (from [[Antiderivative#3. Step-by-Step Example Problems#Example 1 A Single Power Term|Example 1]]). This gives us:

$$\int x^2 \, dx = \frac{x^3}{3} + C$$

- **Step 3:** Bring the $3$ back and multiply using the [[Constant Multiple Rule#Step 4 Reintegration of the Constant]] for integration: 

$$3 \times \left(\frac{x^3}{3}\right)=\frac{3x^3}{3}$$

- **Step 4:** 

The $3$ in the numerator and the $3$ in the denominator cancel each other out, leaving $x^3$.
    
- **Step 5:** Add the constant $C$.
    

$$\int 3x^2 \, dx = x^3 + C$$

### Example 3: Integrating a Constant

Find the antiderivative of a standalone number, like $5$.

A constant can be written as being multiplied by $x^0$ (since $x^0 = 1$).

- **Step 1:** Apply the power rule to $5x^0$.
    
- **Step 2:** Add $1$ to the exponent: $0 + 1 = 1$.
    
- **Step 3:** Divide by the new exponent: $\frac{5x^1}{1} = 5x$.
    
- **Step 4:** Add the constant $C$.
    

$$\int 5 \, dx = 5x + C$$

_Logic check: The derivative of $5x$ is $5$, confirming the antiderivative is correct._

## 4. Solving the Original Polynomial

When an expression has multiple terms separated by plus or minus signs, you simply integrate each term individually, one by one.

Here is the exact breakdown of the function from the definite integral problem: $3x^2 - 4x + 5$.

$$\int (3x^2 - 4x + 5) \, dx$$

1. **First Term ($\int 3x^2 \, dx$):** As shown in Example 2, this becomes **$x^3$**.
    
2. **Second Term ($\int -4x \, dx$):** The exponent on $x$ is $1$. Add $1$ to get $2$, then divide by $2$. This results in $-\frac{4x^2}{2}$, which simplifies to **$-2x^2$**.
    
3. **Third Term ($\int 5 \, dx$):** As shown in Example 3, a constant simply gains an $x$, becoming **$5x$**.
    

Combine the results and add the final constant $C$:

$$\int (3x^2 - 4x + 5) \, dx = x^3 - 2x^2 + 5x + C$$

This resulting function, $F(x) = x^3 - 2x^2 + 5x$, is what is evaluated at the boundaries ($0$ and $2$) to determine the exact area in a definite integral problem.