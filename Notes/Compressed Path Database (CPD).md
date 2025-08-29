A CPD is an all-pairs shortest paths (APSPs) oracle

Having its data compressed, as naive encodings of APSP data are
prohibitively large.

Achieved a state-of-the-art speed performance for problems with static targets and was a top performer in two Grid-based Path Planning Competitions with moving targets and in dynamic environments.

### Pros
- CPDs compute individual first-moves in nanoseconds.
- We can extract entire paths or arbitrary prefixes.
- In static worlds, CPDs can eliminate runtime search.
- In dynamic worlds, CPDs can provide strong bounds (next week!)
- The databases can be thounds of times smaller than full APSP data.

### Cons
- APSP precomputes can be prohibitive.
- Not all state-spaces compress well.

## How to Build a CPD

### Preprocessing

1. Run [[Dijkstra's Algorithm]] repeatedly, once for each [[Node]]
2. After each Dijkstra search, store all the first-move data

### Storage

A naive encoding of APSP data is prohibitively large (often more than the
size of available [[Memory]]). 

We need to reduce the size, but:
- Without losing any information (i.e. lossless compression) and,
- While maintaining fast lookup performance

### Compression Schemes

The best performers currently are based on [[Run-length Encoding]].