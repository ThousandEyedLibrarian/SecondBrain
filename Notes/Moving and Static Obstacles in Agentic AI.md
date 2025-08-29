## Types

- Temporal obstacles can appear and disappear
- Temporal obstacles can move along fixed trajectories
	- The complete movement plan of each obstacle is known a priori
- Other previously planned agents can be obstacles
- Obstacles can operate on a schedule (e.g. doors in a game)

## Collisions

During search we prune any successor-generating moves that would produce collisions with any (static or) temporal obstacle

Two types of collisions we need to consider:
1. Vertex collisions occurs when both agent and obstacle attempt to occupy the same location at the same time
2. Edge collisions occur when both agent and obstacle attempt to simultaneously traverse an edge in opposite directions.

## [[Safe Interval Path Planning (SIPP)]]