#math #calculus #integrals 

https://www.cuemath.com/calculus/constant-multiple-rule/

> The **constant multiple rule** is a general rule that is used in [[Calculus]] when an operation is applied on a function multiplied by a constant. 
> 
> We have different constant multiple rules for differentiation, limits, and [[Integrals|Integration]] in calculus. The general statement of the constant multiple rule is when an operation (differentiation, limits, or integration) is applied to the product of a constant and a function, then it is equal to the product of the constant and operation applied on the function.

### Why do we isolate the constant?

The [[Integrals|integral]] operator ($\int \dots dx$) is a function that only processes variables that match the [[Differential]] ($dx$). **It acts exclusively on the changing parts of a function**.

Constants are "immune" to this operation. By pulling the constant out using the **Constant Multiple Rule**, you are explicitly isolating the variable so the [[Power Rule]] can operate cleanly on it without interference. Once the integration machinery finishes processing the variable, you multiply the untouched constant back into the new result.

--- 

## The Antiderivative of $4x^3$

#### The Constant Multiple Rule

$$\int 4x^3 \, dx$$

**Step 1: The Initial State**

We start with a function that contains both a constant multiplier ($4$) and a variable base with an exponent ($x^3$).

**Step 2: The Constant Multiple Rule**

We extract the constant $4$ outside of the integral operator. This isolates the $x^3$ so we can process it cleanly.

$$4 \cdot \left[ \int x^3 \, dx \right]$$

**Step 3: The [[Power Rule]] for Integration**

We execute the integration exclusively on the isolated variable part. We add $1$ to the exponent ($3 + 1 = 4$) and divide by that new exponent ($4$).

$$\int x^3 \, dx = \frac{x^4}{4}$$

##### Step 4: Reintegration of the Constant

Now that the integral operator has finished its job, we bring the constant $4$ back down and multiply it by our newly integrated term.

$$4 \cdot \left( \frac{x^4}{4} \right)$$

**Step 5: Algebraic Simplification**

We evaluate the explicit multiplication. The $4$ in the numerator and the $4$ in the denominator are inverse operations, so they cancel out completely.

$$\frac{4x^4}{4} = x^4$$

**Step 6: The Constant of Integration**

Because this is an indefinite integral, we append $+ C$ to represent any unknown constant that might have been destroyed if this function was originally differentiated.

$$x^4 + C$$

Would you like to see this exact same "maximum expansion" applied to a limit or a derivative next, to complete your notes for how this rule applies across all three concepts?