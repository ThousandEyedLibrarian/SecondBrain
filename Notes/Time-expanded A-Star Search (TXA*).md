![[Screenshot 2025-08-19 at 15.48.11.png]]

How do we improve performance?

We know [[Heuristic]]s substantially improve search performance. But time-expanded heuristics are expensive!

We will use a relaxed heuristic instead, which simply ignores temporal effects.
- Any strong 2D heuristic works (DH, CPD etc)
- Some suggest computing the 2D heuristic entirely online

Note: Because time is unbounded TXA* might never terminate. For this reason
we say that the algorithm is only solution complete.

## Online 2D Heuristic

Run [[Uniform Cost Search (UCS)]] backwards (i.e. follow incoming edges) to compute a perfect 2D distance table, from every [[Node]] to the target.

### Pros
- Very strong estimates (= fast search)
- Reusable if the source changes more than the target
### Cons:
- UCS runs online, before TXA* search.
- Caching tables for many targets quickly grows prohibitive