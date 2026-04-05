The problem: Given a weighted complete graph $G = (V, E)$ and a Hamiltonian cycle (tour) $T$, decide whether $T$ is a minimal (i.e., shortest) TSP tour.

1. The problem is in coNP:

The complement of the problem asks: Is there another tour $T'$ such that $\text{weight}(T') < \text{weight}(T)$? This is in NP, because a certificate would be another tour $T'$ with smaller weight, which can be checked in polynomial time.

2. The problem is coNP-hard:

The complement problem is equivalent to the usual TSP decision problem: Given $G$ and integer $k$, is there a tour of total weight less than $k$? This is known to be NP-complete. Given a candidate tour $T$ of weight $k$, determining whether there is a better tour is exactly the complement of the problem of deciding whether $T$ is minimal.

Therefore, the problem is coNP-complete.