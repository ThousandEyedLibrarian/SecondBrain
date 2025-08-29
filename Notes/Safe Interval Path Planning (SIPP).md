SIPP is an [[A-Star Search]]-based temporal path planner that flattens the time dimension by grouping together similar [[Node]]s that all involve waiting.

- Nodes are contiguous intervals of time-indexed states.
- Each interval is assigned a g -value
- Successors are intervals from grid/graph adjacent locations.
- The cost of moving is action duration + unavoidable waiting.
- Terminate when Open is exhausted or when goal is safely reached.

SIPP is applicable to any moving obstacle ([[Moving and Static Obstacles in Agentic AI]]) problem including those with positive real-valued action durations.

Pros:
- Much faster than [[Time-expanded A-Star Search (TXA*)]] (due to interval reasoning)
- Guaranteed termination (no time horizon parameter)
- Eliminates many temporally redundant and symmetric paths

Cons:
- Obstacles with unbounded trajectories are tricky
- Inbuilt tie-breaker (wait as late as possible) not always idea