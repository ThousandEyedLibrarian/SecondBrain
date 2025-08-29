Given some environment we need to discretise that to a representation digestible by [[Artificial Intelligence (AI)]] models, e.g. a gridmap, visibility graph or other.

In search [[Algorithms]], we reason about paths by exploring [[Trees]] or [[Graphs]]. But the task environment may not be given as a tree or graph.

Ideally the discretisation should be:
- Fast to create (only relevant for dynamic settings)
- Fast to update (only relevant for dynamic settings)
- Fast to insert (start and target)
- Fast to search
- Representationally complete
- Optimality preserving

## Gridmaps

![[Screenshot 2025-08-19 at 15.22.57.png]]

- Simple to understand, fast to construct, with constant time insertion and easy updates.
- However, only a rough approximation, higher resolution (more squares) can helps but also increases state space

▶ Fast to create? Yes — Θ(n)
▶ Fast to update? Yes — Θ(1)
▶ Fast to insert? Yes — Θ(1)
▶ Fast to search? ?? — Θ(|V | log |V | + |E | log |V |)
▶ Complete? ??
▶ Optimal? ??
?? = Depends on the input obstacles and on the grid resolution

## Visibility Graphs

![[Screenshot 2025-08-19 at 15.22.32.png]]

- Each corner is given a vertex and the edges are normally many $|V| * |V|$ 
- Updating is usually tricky and slow

***Lemma***: optimal paths are direct or turn only at corner points.
▶ Fast to create? No — Θ(|V |2)
▶ Fast to insert? No — O(|V |)
▶ Fast to update? No — O(|V |2)
▶ Fast to search? ?? — Θ(|V | log |V | + |E | log |V |).
▶ Complete? Yes
▶ Optimal? Yes
?? = Depends on the branching factor. O(|E |) = |V |2

## Navigation Meshes

![[Screenshot 2025-08-19 at 15.21.55.png]]

- Divide the traversable space into large convex polygons
- Insert and update are both efficient, requiring only local operations

▶ Fast to construct? Yes — O(n log n)
▶ Fast to insert? Yes — O(log |V |)
▶ Fast to update? Yes — between Ω(log |V |) and O(|V |)
▶ Fast search? Yes — Exact bound depends on the type of mesh
▶ Complete? Yes
▶ Optimal? ??
?? = No for door and polygon adjacency graphs.
Yes for path planners that search directly on the mesh.


See also:
- [[Dijkstra's Algorithm]]
- [[A-Star Search]]
- [[Compressed Path Database (CPD)]]
- [[Graph Search]]