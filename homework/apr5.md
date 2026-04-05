The problem is in NP: Given a string $w$, we can check whether $ww$ is accepted by a given NFA $A$ in polynomial time. We nondeterministically guess a string $w$ of length at most $n$ (where $n$ is the number of states of $A$), compute $ww$, and simulate $A$ on $ww$.

To prove NP-hardness, we reduce from the Hamiltonian Cycle problem. Suppose we have a directed graph $G = (V, E)$ with vertices $V = \{1, \dots, n\}$. We construct an NFA $A$ over the alphabet $\Sigma = V \cup \{c\}$, where $c$ is a new symbol not in $V$. The NFA $A$ has the following property: $A$ accepts a string of the form $w c w$ if and only if $w = v_1 v_2 \dots v_n$ is a permutation of the vertices, $(v_1, v_2), (v_2, v_3), \dots, (v_n, v_1) \in E$, and there are no repeats in $w$. In short, $w$ corresponds to a Hamiltonian cycle in $G$.

- The NFA guesses the first part $w$, making sure each vertex is used exactly once and consecutive pairs are edges in $E$.
- After reading the separator symbol $c$, the NFA checks that the second part of the input exactly matches the first part, symbol by symbol.

If $G$ has a Hamiltonian cycle, then $A$ will accept a string of the form $w c w$, so there is a $w$ such that $ww \in L(A)$. Conversely, if such a string is accepted by $A$, it encodes a Hamiltonian cycle in $G$.

The NFA square problem is NP-complete.