https://en.wikipedia.org/wiki/Phase_(waves)

>In [physics](https://en.wikipedia.org/wiki/Physics "Physics") and [mathematics](https://en.wikipedia.org/wiki/Mathematics "Mathematics"), the **phase** (symbol φ or ϕ) of a [wave](https://en.wikipedia.org/wiki/Wave_\(physics\) "Wave (physics)") or other [periodic function](https://en.wikipedia.org/wiki/Periodic_function "Periodic function") F![{\displaystyle F}](https://wikimedia.org/api/rest_v1/media/math/render/svg/545fd099af8541605f7ee55f08225526be88ce57) of some [real](https://en.wikipedia.org/wiki/Real_number "Real number") variable t![{\displaystyle t}](https://wikimedia.org/api/rest_v1/media/math/render/svg/65658b7b223af9e1acc877d848888ecdb4466560) (such as time) is an [angle](https://en.wikipedia.org/wiki/Angle "Angle")-like quantity representing the fraction of the cycle covered up to t![{\displaystyle t}](https://wikimedia.org/api/rest_v1/media/math/render/svg/65658b7b223af9e1acc877d848888ecdb4466560). It is expressed in such a [scale](https://en.wikipedia.org/wiki/Scale_\(ratio\) "Scale (ratio)") that it varies by one full [turn](https://en.wikipedia.org/wiki/Turn_\(geometry\) "Turn (geometry)") as the variable t![{\displaystyle t}](https://wikimedia.org/api/rest_v1/media/math/render/svg/65658b7b223af9e1acc877d848888ecdb4466560) goes through each [period](https://en.wikipedia.org/wiki/Period_\(physics\) "Period (physics)") (and F(t)![{\displaystyle F(t)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/5b57ed3bbf501fb3c7f4bc5c4eafa96bb9e32165) goes through each complete cycle). It may be [measured](https://en.wikipedia.org/wiki/Measure_\(mathematics\) "Measure (mathematics)") in any [angular unit](https://en.wikipedia.org/wiki/Angular_unit "Angular unit") such as [degrees](https://en.wikipedia.org/wiki/Degree_\(angle\) "Degree (angle)") or [radians](https://en.wikipedia.org/wiki/Radians "Radians"), thus increasing by 360° or 2π![{\displaystyle 2\pi }](https://wikimedia.org/api/rest_v1/media/math/render/svg/73efd1f6493490b058097060a572606d2c550a06) as the variable t![{\displaystyle t}](https://wikimedia.org/api/rest_v1/media/math/render/svg/65658b7b223af9e1acc877d848888ecdb4466560) completes a full period.[[1]](https://en.wikipedia.org/wiki/Phase_\(waves\)#cite_note-Ballou2005-1)

## Mathematical Definition

Let the signal $F$ be a periodic function of one real variable, and $T$ be its period (that is, the smallest positive real number such that $F(t + T) = F(t)$ for all $t$).

Then the phase of $F$ at any argument $t$ is:

$$\varphi(t) = 2\pi \left[\kern-0.15em\left[ \frac{t - t_0}{T} \right]\kern-0.15em\right]$$

Here, $[\![\,\cdot\,]\!]$ denotes the fractional part of a real number, discarding its integer part; that is:

$$[\![x]\!] = x - \lfloor x \rfloor$$

The variable $t_0$ is an arbitrary "origin" value of the argument, which is considered to be the beginning of a cycle.

This concept can be visualized by imagining a clock with a hand that turns at a constant speed, making a full turn every $T$ seconds, and pointing straight up at time $t_0$. The phase $\varphi(t)$ is then the angle from the 12:00 position to the current position of the hand at time $t$, measured clockwise.

The phase concept is most useful when the origin $t_0$ is chosen based on features of $F$. For example, for a sinusoid, a convenient choice is any $t$ where the function's value changes from zero to positive.

The formula above gives the phase as an angle in radians between $0$ and $2\pi$. To get the phase as an angle between $-\pi$ and $+\pi$, one instead uses:

$$\varphi(t) = 2\pi \left( \left[\kern-0.15em\left[ \frac{t - t_0}{T} + \frac{1}{2} \right]\kern-0.15em\right] - \frac{1}{2} \right)$$

The phase expressed in degrees (from 0° to 360°, or from −180° to +180°) is defined the same way, except with "360°" in place of "$2\pi$".
