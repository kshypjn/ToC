
### PSPACE-membership

NFA-Equivalence is in PSPACE.  
Specifically, it is in PSPACE because its complement---NFA non-equivalence ("Does there exist $w \in \Sigma^*$ such that $A(w) \neq B(w)$?")---is in PSPACE.

Let us outline a nondeterministic polynomial space procedure:

- Guess a string $w$ of length up to $2^{n}$, where $n$ is the total number of states in $A$ and $B$.
- Simulate both $A$ and $B$ on $w$, using a polynomial amount of space to track the current subsets of states for both NFAs.
- Accept if $w$ is accepted by exactly one of $A$ or $B$.

By Savitch's Theorem, NPSPACE $=$ PSPACE, so this can be done in PSPACE.  
Hence, NFA-Equivalence is in PSPACE.

### PSPACE-hardness

To show PSPACE-hardness, we reduce the NFA-Universality problem (known to be PSPACE-complete) to NFA-Equivalence.

Recall: Given an NFA $A$ over $\Sigma$, NFA-Universality asks whether $L(A) = \Sigma^*$.  
We can construct another NFA $B$ that recognizes $\Sigma^*$ (for example, a single-state NFA that accepts every input).

Notice that $L(A) = \Sigma^*$ if and only if $L(A) = L(B)$.

Thus, NFA-Universality reduces in polynomial time to NFA-Equivalence.  
Since NFA-Universality is PSPACE-hard, so is NFA-Equivalence.
