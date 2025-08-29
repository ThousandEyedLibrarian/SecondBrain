Requires a collision-free plan that moves a team of agents, often with certain constraints.

Each agent begins at a specific start point and needs to get to a specific end point, moving on a 4-connected grid with all actions incurring the same unit cost (waiting is allowed but counts as an action).

**The key objectives are:**
1. Sum of Costs: Minimise the total cost of all assigned paths
2. Makespan: Minimise the arrival time of the last agent

**Constraints:**
1. Two agents cannot occupy the same grid cell at the same time or swap positions at the same time
2. Agents can move in lockstep
3. Agents arrive at their destination if they can remain their collision-free

![[Screenshot 2025-08-29 at 11.50.29.png]]

MAPF is intractable in a large number of cases but not always, specifically general directed/undirected graphs and general grid graphs are unlikely to have polynomial time algorithms.

Bi-directional graphs and well-formed instances are likely to have polynomial time solutions.

## MAPF Approaches

### Centralised

Agents are planned together by a single controller
- Coupled: Agents planned jointly
- Decoupled: Agents planned independently, subject to contraints

### Distributed

Agents are planned independently without global knowledge
- Each agent has its own model of the environment and plants for itself then executes
- Conflicts are detected during execution and agents replan
- Local information sharing and local negotiation (optional)

## MAPF Algorithms

- [[Centralised A-Star (CA*)]] 
- [[Operator Decomposition (OD)]]
- [[Independence Detection (OD+ID)]]
- [[Conflict-based Search (CBS)]]

**Symmetry Breaking**
- Automatic symmetry detection
	- Zhang, H., Li, J., Surynek, P., Kumar, T.K.S. and Koenig, S., 2022. Multi-agent path finding with mutex propagation. Artificial Intelligence.

**High-Level Heuristics**
- Pairwise reasoning
	- Felner, A., Li, J., Boyarski, E., Ma, H., Cohen, L., Kumar, T.K.S. and Koenig, S., 2018. Adding heuristics to conflict-based search for multi-agent path finding. In Proceedings of ICAPS.
- Li, J., Felner, A., Boyarski, E., Ma, H. and Koenig, S., 2019. Improved heuristics for multi-agent path finding with conflict-based search. In Proceedings of IJCAI.
- Beyond pairwise reasoning
	- Shen, B., Chen, Z., Li, J., Cheema, M.A., Harabor, D. and Stuckey, P.J., 2023. Beyond pairwise reasoning in multi-agent path finding. In Proceedings of ICAPS.

