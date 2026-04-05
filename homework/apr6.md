Consider the following problem: Given a nondeterministic finite automaton (NFA) $A = (Q, \Sigma, \delta, q_0, F)$ and an integer $N$, does there exist a string $w \in \Sigma^N$ (that is, a string of length exactly $N$) such that $A$ accepts $w$?

We can solve this problem in time polynomial in the size of the NFA (i.e., $|Q|$, $|\Sigma|$, and the size of $\delta$) and $N$ as follows:

Define $S_k \subseteq Q$ to be the set of states that $A$ can reach from the start state $q_0$ by reading some string of length $k$ (for $k = 0, 1, \ldots, N$).

We can compute these sets iteratively:
- Initialize $S_0 = \{ q_0 \}$.
- For $k = 1$ to $N$:
    - $S_k = \bigcup_{q \in S_{k-1}} \bigcup_{a \in \Sigma} \delta(q, a)$

After $N$ steps, $S_N$ contains all states reachable from $q_0$ along a path labeled by some string of length $N$.

Finally, check whether $S_N$ contains any accepting state: if $S_N \cap F \neq \emptyset$, then there exists a string of length $N$ accepted by $A$.

Each computation of $S_k$ from $S_{k-1}$ involves considering all states and all input symbols, so the total running time is $O(N \cdot |Q| \cdot |\Sigma|)$. This is polynomial in the size of the NFA and $N$.

Thus, the problem can be solved in polynomial time.