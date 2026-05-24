#math #algorithms #ai #graph_theory

In computer science and pathfinding, a **heuristic** is a "rule of thumb" or an educated guess used to guide an algorithm toward a solution more efficiently. 

While algorithms like **[[Dijkstra's Algorithm]]** explore in every direction equally, an **Informed Search** (like **A***) uses a heuristic to prioritize the most promising paths.

---

## 1. The Heuristic Function $h(n)$
In pathfinding, $h(n)$ represents the **estimated cost** from the current node $n$ to the goal.

### Admissibility
A heuristic is said to be **admissible** if it never overestimates the actual cost to reach the goal. Admissibility is required for algorithms like A* to be guaranteed to find the absolute shortest path.

---

## 2. Common Pathfinding Heuristics

### A. Manhattan Distance
Used when movement is restricted to 4 directions (Up, Down, Left, Right), like on a square grid. It is the sum of the absolute differences of the coordinates.
$$h(n) = |x_1 - x_2| + |y_1 - y_2|$$

### B. Euclidean Distance
The straight-line "as the crow flies" distance. Used when movement is possible at any angle.
$$h(n) = \sqrt{(x_1 - x_2)^2 + (y_1 - y_2)^2}$$
*(Note: This is the same as the [[Magnitude]] of the vector connecting the two points.)*

### C. Chebyshev Distance
Used when diagonal movement is allowed and has the same cost as horizontal/vertical movement (like a King in Chess).
$$h(n) = \max(|x_1 - x_2|, |y_1 - y_2|)$$

---

## 3. Usage in A* Search
The A* algorithm uses the formula:
$$f(n) = g(n) + h(n)$$

- $g(n)$: The actual cost to get from the start to the current node.
- $h(n)$: The **heuristic** estimate to get from the current node to the goal.
- $f(n)$: The total estimated cost of the path through node $n$.

By choosing the node with the lowest $f(n)$, the algorithm "pulls" the search toward the goal instead of wasting time exploring in the opposite direction.

---

## 4. Programming Example (Pseudocode)
```rust
fn heuristic(current: Point, goal: Point) -> f64 {
    // Manhattan Distance for a grid-based game
    ((current.x - goal.x).abs() + (current.y - goal.y).abs()) as f64
}
```

---

## Related Concepts
* [[Euclidean]]
* [[Graph Theory]]
* [[Magnitude]]
* [[Vectors]]
* [[Numerical Linear Algebra]]
