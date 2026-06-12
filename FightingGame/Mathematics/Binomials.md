#math #algebra 

> A [[Polynomial]] with 2 [[Terms]].

# Conjugate

> In mathematics, a **binomial conjugate** is ==a pair of two-term algebraic expressions that are identical _**except**_ for the operational sign ($+$ or $−$) separating their terms==. For example, the conjugate of the binomial $(a + b)$ is $(a - b)$. You just flip the signs.

### 1. The Difference of Squares Property
The defining algebraic property of binomial conjugates is that their product always yields a difference of two squares:

$$(a+b)(a-b)=a^{2}-b^{2}$$

When using the FOIL method to multiply them, the outer and inner terms are opposites ($-ab$ and $+ab$) and perfectly cancel each other out:

$$(a+b)(a-b)=a^{2}-ab+ab-b^{2}=a^{2}-b^{2}$$

### 2. Rationalization of Radicals (Surds)
When working with irrational radical binomials (surds), multiplying an expression by its conjugate eliminates the radical completely. This property is used heavily to rationalize denominators.

* **Property:** $(\sqrt{x} + \sqrt{y})(\sqrt{x} - \sqrt{y}) = x - y$
* **Example:** To simplify a fraction with $\sqrt{5} + \sqrt{3}$ in the denominator, you multiply the numerator and denominator by its conjugate, $\sqrt{5} - \sqrt{3}$. The resulting denominator becomes a clean rational integer:
  $$(\sqrt{5})^2 - (\sqrt{3})^2 = 5 - 3 = 2$$

### 3. Complex Numbers and the Real Product Property
A complex number $a + bi$ is technically a binomial. Its complex conjugate is $a - bi$.

* **The Real Product Property:** Multiplying a complex binomial by its conjugate always yields a purely real number.
  $$(a+bi)(a-bi)=a^{2}-(bi)^{2}=a^{2}-b^{2}i^{2}$$
  Since $i^2 = -1$, the formula simplifies to the sum of squares:
  $$(a+bi)(a-bi)=a^{2}+b^{2}$$
* **The Real Sum Property:** Adding a complex binomial to its conjugate also cancels out the imaginary component, resulting in a real number:
  $$(a+bi)+(a-bi)=2a$$

### 4. Conjugate Root Theorem
In polynomial algebra, binomial conjugates govern the behavior of polynomial roots.

* **Irrational Roots:** If a polynomial has rational coefficients and $a + \sqrt{b}$ is a root, then its conjugate $a - \sqrt{b}$ must also be a root.
* **Complex Roots:** If a polynomial has real coefficients and a complex binomial $a + bi$ is a root, its complex conjugate $a - bi$ must also be a root.
