#math #statistics #probability

# Statistics and Probability

This field deals with the collection, analysis, interpretation, and presentation of data, as well as the modeling of uncertainty.

---

## 1. Probability Basics
Probability measures the likelihood of an event occurring, ranging from $0$ (impossible) to $1$ (certain).

### Bayes' Theorem
Describes the probability of an event based on prior knowledge of conditions that might be related to the event.
$$P(A|B) = \frac{P(B|A)P(A)}{P(B)}$$

---

## 2. Distributions
- **[[Gaussian|Normal Distribution (Gaussian)]]:** The "Bell Curve." Most natural phenomena follow this.
- **Uniform Distribution:** Every outcome is equally likely (like a fair die).

---

## 3. Markov Chains
A stochastic model describing a sequence of possible events in which the probability of each event depends only on the state attained in the previous event.

* **Matrix Connection:** Markov chains are often calculated using a **Transition Matrix**. If you multiply the current state vector by the transition matrix, you get the probability of the next state.

---

## 4. Randomness in Graphics
- **Monte Carlo Integration:** Used in [[Simple Raytracing]] to calculate complex lighting by shooting thousands of random rays and averaging the result.
- **Stochastic Noise:** Related to [[Perlin Noise]] for generating procedural terrain.

---

## Related Concepts
* [[Chaitin's Constant]]
* [[Matrices]]
* [[Perlin Noise]]
* [[Simple Raytracing]]
