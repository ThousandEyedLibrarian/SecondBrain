
Weighted A* is actually a family of related [[Algorithms]].
- w = 0 → [[Uniform Cost Search]]
- w = 1 → [[A-Star Search]]
- w = ∞ → [[Greedy Best-First Search]]

## Pros and Cons

Bad news:
- Heuristic estimates might overestimate the cost-to-go (inadmissible).
- Heuristic estimates might also be inconsistent.

Good news:
- Search now progresses more quickly toward the goal.
- We obtain feasible solutions sooner.
- Solution cost guaranteed: at most w -times larger than optimal.
- Re-expansions are not required to achieve the guarantee.

## Anytime Weighted A*

Weighted A* terminates after finding the first solution. But the search could also continue to optimality or until some time limit.

Gist:
- Upper-bound (UB): the cost of the best solution thus far.
- Lower-bound (LB): unweighted f-value of the best node on Open.
- Keep expanding while LB < UB.
- Re-expand nodes if their g-value can be improved.
- Update UB every time the goal is expanded anew.
- Terminate out of time or when Open is exhausted.