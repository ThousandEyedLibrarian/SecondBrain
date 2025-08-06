Pseudo-code example courtesy of Monash University

![[Screenshot 2025-08-06 at 12.56.23.png]]

To avoid re-expanding [[Node]]s we introduce a Closed list: a data structure that remembers every node expanded thus far.

To avoid suboptimal expansions we also add a relax operation that updates the priorities of successors already on Open.

Relaxing a node n ∈ Open means:
- We update g (n) to be the smaller of the two costs
- We update the parent of n as necessary
- We update the priority of n on the Open list.

Advantages of Graph-Search:
- Strong guarantees (Complete & always optimal; e.g. with [[Uniform Cost Search]])
- Fewer expansions to prove optimality.
- Better space complexity: O(|V |) vs O(bd ) (or worse)

Disadvantages of Graph-Search
- Possible timeouts (proving things can be hard!)
- Possible memoryouts (storing the Closed list can be prohibitive)

As a general rule, for polynomial domains we prefer Graph-Search and for exponential domains we prefer (depth-limited/iterative) [[Tree Search]].