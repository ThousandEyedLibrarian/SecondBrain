A searching [[Algorithms]] that works by expanding the 'cheapest' [[Node]] first. 

Processes all nodes with a cost less than the existing cheapest solution. Normally the optimal algorithm for pathfinding, [[Agents]] searches etc.

Time Complexity: $O(b1+⌊C ∗/ϵ⌋)$ — assuming ϵ > 0.
Space Complexity: $O(b1+⌊C ∗/ϵ⌋)$ — assuming ϵ > 0.

So what's the problem here? It's blind, it has no clue where the goal state is from any given point.

So we make it *informed* by adding a [[Heuristic]].

See also:
- [[Planning Agents]]
- [[Rational Agents]]
- [[Graph Search]]