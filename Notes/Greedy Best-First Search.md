A variant of [[Uniform Cost Search]] wherein a [[Heuristic]] ($h(n)$)is added based on the priority of each [[Node]] (the [[Manhattan Distance]]).

At each step, we expand the most promising node according to $h_M$.

Unfortunately this is often a suboptimal [[Algorithms]], and in [[Tree Search]] may not even terminate. So we move to [[A-Star Search]].