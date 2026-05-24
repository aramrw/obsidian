#shaders #computer_graphics #math 
> the `abs()` function computes the absolute value of a number. It removes the negative sign, returning only the magnitude.
> 
> Mathematically, it is defined as $f(x) = |x|$. If a value is negative, it becomes positive. If it is already positive, it remains unchanged.
> 
> In the context of shaders, `abs()` functions as a spatial mirror.
> 
> When you apply it to a coordinate space—such as `abs(uv.x)`—you destroy the negative domain and replace it with a reflection of the positive domain. Whatever geometric logic you construct on the right side of the axis is instantly mirrored on the left. It enforces perfect symmetry across the axis without requiring duplicate rendering logic.