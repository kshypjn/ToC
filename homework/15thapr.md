NFA Universality Problem: Given a nondeterministic finite automaton (NFA) $A$ over alphabet $\Sigma$, is $L(A) = \Sigma^*$? (i.e., does $A$ accept all possible strings?)

We claim that NFA Universality is PSPACE-complete.

PSPACE-hardness:

We show that the problem is PSPACE-hard by reducing the PSPACE-complete problem of DFA non-emptiness for polynomial space bounded Turing machines (or, more concretely, by reduction from the complement of DFA non-universality or from regular expression universality, both known to be PSPACE-complete).

Alternatively, we can show NFA universality is PSPACE-hard via a reduction from the regular expression universality problem (known to be PSPACE-complete):

Given a regular expression $R$ over $\Sigma$, is $L(R) = \Sigma^*$?

Since regular expressions can be converted to NFAs of polynomial size, we can reduce regular expression universality to NFA universality in polynomial time.

Thus, NFA Universality is PSPACE-hard.

PSPACE-membership:

We show NFA Universality is in PSPACE.

Observe that $L(A) = \Sigma^*$ iff $A$ does not reject any string, i.e., for all $w \in \Sigma^*$, $w \in L(A)$. Equivalently, $L(A)$ is not missing any string.

To check non-universality, it suffices to check if there exists $w \in \Sigma^*$ such that $A$ rejects $w$. That is, check if $\Sigma^* \setminus L(A) \neq \emptyset$.

Recall that the non-universality problem is "Is there a string not accepted by $A$?" This is equivalent to NFA non-universality, which is in PSPACE.

Algorithm for NFA non-universality:

- The shortest string $w$ not accepted by $A$ is at most exponential in the size of $A$, because all the possible subsets of states can be represented with at most $2^{n}$ states in the determinized version.
- However, we cannot build the DFA explicitly, as it would be exponentially big. But we can search for such a string in PSPACE.

We can use the following nondeterministic polynomial space algorithm:

1. Nondeterministically guess a string $w$ of length up to $2^{n}$.
2. Simulate the NFA on $w$ step by step, using only the current set of states (needs $O(n)$ space).
3. Accept if $w$ is not accepted by $A$.

By Savitch's Theorem, NPSPACE = PSPACE.

Therefore, NFA Universality is in PSPACE.

