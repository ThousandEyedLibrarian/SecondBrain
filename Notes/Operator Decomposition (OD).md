Agents select compatible moves one at a time in some fixed order, after $|A|$ individual moves, the search advances one timestep.

![[Screenshot 2025-08-29 at 11.57.45.png]]

- Branching factor reduced to $b = 5$ on 4-C gridmaps ([[Discretising An Environment For AI Models]])
- Solutions are deeper in the tree (from $d$ with [[Centralised A-Star (CA*)]] to $d \times |A|$)
- Complete and optimal
- Works well for problems with small numbers of agents
