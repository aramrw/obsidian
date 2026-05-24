#math #discrete_math #algorithms

# Graph Theory

Graph theory is the study of **graphs**, which are mathematical structures used to model pairwise relations between objects.

---

## 1. Definitions
A graph $G = (V, E)$ consists of:
- **Vertices (Nodes):** $V$ is a set of points.
- **Edges (Links):** $E$ is a set of lines connecting these points.

### Types of Graphs
- **Directed Graph (Digraph):** Edges have a direction (arrows).
- **Undirected Graph:** Edges are bidirectional.
- **Weighted Graph:** Edges have values (e.g., distance, cost).

---

## 2. The Adjacency Matrix
A graph can be represented as a [[Matrices|matrix]]. If there are $N$ nodes, an $N \times N$ matrix is created where the entry at $(i, j)$ is $1$ if an edge exists between node $i$ and node $j$, and $0$ otherwise.

---

## 3. Pathfinding Algorithms
Graph theory is famous for solving the "shortest path" problem:
- **[[Dijkstra's Algorithm]]**: Finds the shortest path in a weighted graph.
- **A* Search**: An optimized version using [[Heuristics]] (used in almost every video game for NPC movement).

---

## 4. Trees
A **Tree** is a special type of graph where any two vertices are connected by exactly one path (no cycles).
- **In Computing:** Used for file systems, scene trees (in Godot/Unity), and decision trees in AI.

---

## Related Concepts
* [[Matrices]]
* [[Vectors and Matrices]]
* [[Numerical Linear Algebra]]
