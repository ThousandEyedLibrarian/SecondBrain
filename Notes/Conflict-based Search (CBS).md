An optimal branch-and-replan [[Algorithms]].

![[Screenshot 2025-08-29 at 12.02.58.png]]

- For each valid solution S, there exists a node N on Open which permits S.
	- Trivially true at the root node (no constraints)
	- Each split divides the set of valid solutions at the parent node.
	- Constraints eliminate valid solutions from one subtree or the other but never from both.
- Each node N is a minimum cost plan where the paths of the agents are consistent with the set of constraints at N
- The minimum f-value of any node N ∈ Open is lower-bound on the minimum cost of any valid solution.