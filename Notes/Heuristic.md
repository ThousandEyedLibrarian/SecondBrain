A heuristic value represents the estimated distance from the current [[Node]] to the goal state node in a graph problem. 

Imagine you’re in a room and you can smell food in the other room. You can just guess how far you are from the food in meters or some other unit of measurement. 

As long as your estimate is equal to or below the actual distance to the food, the [[A-Star Search]] [[Algorithms]] will work. In more complicated settings, like Pacman, you can estimate the distance between objects using something like the [[Manhattan Distance]].

## Properties

- Admissibility: the heuristic never over-estimates the cost-to-go
	- $h(n) ≤ h∗(n)$ where $h∗(n)$ is the true cost from $n$ to $t$.
- Consistency: heuristic estimates decrease monotonically from n to t

## Informedness

- Heuristic $h1$ is less informed than heuristic $h2$ iff for all non-goal nodes $n$ we have $h1(n) < h2(n)$.
- Heuristic $h2$ dominates heuristic h1 $iff$ for all non-goal nodes $n$ we have $h2(n) ≥ h1(n)$.