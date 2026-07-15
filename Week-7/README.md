# Week 7 - DSA Bootcamp 2026

[Home](https://github.com/wncc/DSA-Bootcamp-2026/blob/main/README.md) > Week 7

---

## Learning Path

Week 7 introduces **Graphs** — the most versatile and interview-heavy data structure in DSA. Every tree you've studied is a graph. This week covers how to represent graphs and the two fundamental ways to traverse them. Everything that comes after — shortest paths, topological sort, MST, cycle detection — builds on what you learn here.

```
Graph Representation
    |
    |  A graph is vertices + edges. Before you can traverse it, you need
    |  to store it. Two ways: Adjacency Matrix (O(V²) space, O(1) edge lookup)
    |  and Adjacency List (O(V+E) space, preferred in almost all problems).
    v
BFS (Breadth First Search)
    |
    |  Explore level by level using a Queue. Visits closest vertices first.
    |  Guarantees the shortest path in an unweighted graph.
    |  Handle disconnected graphs by running BFS from every unvisited vertex.
    v
DFS (Depth First Search)
    |
    |  Go as deep as possible before backtracking, using Recursion or a Stack.
    |  Foundation for cycle detection, topological sort, SCCs, bridges,
    |  articulation points, and all backtracking problems on graphs.
    v
Week 8

```

---

## Topics

| # | Topic | What You Will Learn | Est. Time |
|---|-------|---------------------|-----------|
| 1 | [Graph Basics — Representation, BFS, DFS](https://github.com/wncc/DSA-Bootcamp-2026/blob/main/Week-7/graph-basics.md) | Adjacency Matrix vs Adjacency List, BFS (queue, level-order, disconnected graphs), DFS (recursion, stack, backtracking), time complexity O(V+E) | 5–6 hrs |

---

## Problems Roadmap

Week 7 includes a curated problems roadmap inside `graph-basics.md` covering 7 categories:

| Category | Problems |
|----------|----------|
| Traversal | BFS of Graph, DFS of Graph |
| Grid Graphs | Flood Fill, Rotten Tomatoes, Number of Islands |
| Graph Coloring | Check if Bipartite |
| Cycle Detection | Undirected Graph, Directed Graph |
| Topological Sorting | DFS-based, Kahn's Algorithm (BFS) |
| Shortest Paths | Unweighted BFS, Dijkstra, Bellman-Ford, Floyd-Warshall |
| Minimum Spanning Tree | Prim's Algorithm, Kruskal's Algorithm |

Work through the problems in this order — each category builds on the one before it.

---

## Suggested Daily Schedule

| Day | Focus |
|-----|-------|
| 1 | Graph Representation — understand Adjacency Matrix vs List, implement both in C++ |
| 2 | BFS — single component, disconnected graph, implement from scratch |
| 3 | BFS problems — BFS of Graph, Rotten Tomatoes, Number of Islands |
| 4 | DFS — recursive + iterative (stack), backtracking mechanics |
| 5 | DFS problems — DFS of Graph, Flood Fill, Cycle Detection (undirected) |
| 6 | Cycle Detection (directed) + Bipartite Check + Topological Sort |
| 7 | Shortest Path problems — BFS unweighted, Dijkstra, Bellman-Ford |

---

## Before You Move to Week 8

- Can you implement an Adjacency List from scratch in C++ using `vector<vector<int>>`?
- Do you know when to use Adjacency Matrix vs Adjacency List?
- Can you write BFS for a disconnected graph without looking it up?
- Can you write recursive DFS and explain what backtracking means here?
- Do you understand why BFS gives the shortest path in an unweighted graph but DFS doesn't?
- Have you attempted all problems in the roadmap table?

If yes, you are ready. [See you in Week 8.](https://github.com/wncc/DSA-Bootcamp-2026/blob/main/Week-8/README.md)

---

[Home](https://github.com/wncc/DSA-Bootcamp-2026/blob/main/README.md) | [Previous: Week 6](https://github.com/wncc/DSA-Bootcamp-2026/blob/main/Week-6/README.md) | [Next: Week 8](https://github.com/wncc/DSA-Bootcamp-2026/blob/main/Week-8/README.md)
