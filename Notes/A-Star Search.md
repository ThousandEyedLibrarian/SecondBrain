# A* Search

A searching algorithm that combines [[Uniform Cost Search]] and [[Greedy Technique & Algorithms]]. Orders by the sum of greedy search and [[Uniform Cost Search]] (f(n) = g(n) + h(n)).

## Example: Mouse in a Maze

- Imagine a mouse in a maze with cheese at some point
- If the mouse has no sense of smell it will wander aimlessly until it encounters the cheese ([[Uniform Cost Search]])
- If we give the mouse smell, it will be able to sense how correct a given navigation decision was based on the smell decreasing/increasing etc.
	- This is a [[Heuristic]], it allows us to prioritise options when multiple are presented

Let's now model this hypothetical as a graph.

- Each fork in the maze is a [[Graphs]] [[Node]]
- Between each node is a path of course, with a value representing the distance between the two nodes
- We give each node a heuristic (estimated distance to cheese)
- The initial node is added to a [[Queue]] ($visited$) with a value of 0 plus its heuristic value
- We then pop this node off the queue and add its child nodes as their distance values from the previous node plus their heuristic value
- We take the path option with the lowest value and repeat until the goal is found (cheese in this case)

Example image courtesy of Anish Krishnan on YouTube.

![[Screenshot 2025-08-06 at 12.24.00.png]]


## What is a [[Heuristic]]?

See linked page.

## Tie Breaking

Sometimes many nodes have the same f -value. How to decide which node to expand next?

One good strategy: choose the node with smallest h-value (= largest-g), but the smallest-h strategy fails when we allow zero cost actions.

## Performance

In general:
- For any dominant heuristic $h$ there exists a class of A* algorithms $A^∗_h$.
- Each $A^∗_ h ∈ A^∗_ h$ is differentiated from the rest by tie-breaking.
- How to choose the one that always gives optimal efficiency in general is an open problem.

Bottom line:
- A* has the same worst-case performance as UCS.
- With a good heuristic, A* can be much more efficient in practice.
- Many of the currently leading planners employ some type of A* search.

## [[Weighted A-Star Search]]


See also:
- [[Algorithms]]