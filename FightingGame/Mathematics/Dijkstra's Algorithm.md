#math #algorithms #graph_theory

# Dijkstra's Algorithm

Dijkstra's Algorithm is a classic pathfinding algorithm used to find the **shortest path** between nodes in a graph. Unlike [[Heuristics|informed searches]], Dijkstra's is an "uninformed" search—it explores in all directions equally until it finds the goal.

---

## 1. How It Works
Dijkstra's maintains a set of "visited" nodes and a set of "unvisited" nodes. It starts at a source node and iteratively selects the unvisited node with the smallest tentative distance.

### The Steps:
1. Assign a **distance value** of zero to the start node and infinity to all other nodes.
2. Set the start node as the current node.
3. For the current node, consider all its unvisited neighbors and calculate their tentative distances through the current node.
4. Compare the newly calculated tentative distance to the current assigned value and assign the smaller one.
5. Once all neighbors are considered, mark the current node as **visited**.
6. Select the unvisited node with the smallest tentative distance and repeat from step 3.

---

## 2. Dijkstra vs. A*
The main difference is the use of [[Heuristics]].

- **Dijkstra's:** Guaranteed to find the shortest path in a weighted graph (with non-negative weights). It expands in a "circle" from the start.
- **A* Search:** Uses a heuristic to "pull" the search toward the goal, making it much faster in most cases. It is essentially Dijkstra's + a heuristic.

| Feature | Dijkstra's | A* |
| :--- | :--- | :--- |
| **Search Style** | Uniform / Circular | Focused / Directional |
| **Speed** | Slower (explores everything) | Faster (explores promising paths) |
| **Use Case** | When the goal is unknown or multiple goals exist | When the goal position is known |

---

## 3. Mathematical Requirements
For Dijkstra's to work correctly:
- The graph must be **Weighted**.
- Edges must have **Non-negative weights**. If a graph has negative weights, you must use the **Bellman-Ford algorithm** instead.

---

## 4. Programming Example (Pseudocode)
```rust
use std::collections::BinaryHeap;

// A simple priority queue implementation for Dijkstra
fn dijkstra(start: Node, graph: Graph) {
    let mut distances = HashMap::new();
    let mut pq = BinaryHeap::new();

    distances.insert(start, 0);
    pq.push(State { cost: 0, position: start });

    while let Some(State { cost, position }) = pq.pop() {
        if cost > *distances.get(&position).unwrap_or(&usize::MAX) { continue; }

        for neighbor in graph.neighbors(position) {
            let next_cost = cost + neighbor.weight;
            if next_cost < *distances.get(&neighbor).unwrap_or(&usize::MAX) {
                distances.insert(neighbor, next_cost);
                pq.push(State { cost: next_cost, position: neighbor });
            }
        }
    }
}
```

---

## Related Concepts
* [[Graph Theory]]
* [[Heuristics]]
* [[Matrices]] (Adjacency Matrix)
* [[Numerical Linear Algebra]]
