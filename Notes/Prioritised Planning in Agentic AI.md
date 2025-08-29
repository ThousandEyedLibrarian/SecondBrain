See also: [[Multi-Agent Path Finding (MAPF)]]

Pros:
- Simple (one agent at a time)
- Fast (one agent at a time!)

Cons:
- Not optimal
- Not complete in general (certain problem setups avoid this)
- Not clear how to find a good ordering

## Limits of prioritised planning

Some strong restrictions:
- Not every problem is priority solvable
- Among those that are solvable, not all can be solved optimally with prioritised planning
- Even if we know an optimal plan is computable, and even if we have the optimal ordering, we might still fail due to tie-breaking

On the other hand!
- Feasible solutions are often plentiful
- Prioritised plans can be near-optimal in many practical settings
- Some prioritised planners are better than others!


See also:
- [[Moving and Static Obstacles in Agentic AI]]
- [[Planning Agents]]