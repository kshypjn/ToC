Let $\varphi$ be a propositional logic formula. Consider the problem:

Given $\varphi$, is there exactly one satisfying assignment?

### 1. The problem is coNP-hard

We can show coNP-hardness by reducing from the coNP-complete problem UNSAT (unsatisfiability):

Given any formula $\psi$, note that $\psi$ is unsatisfiable if and only if it has zero satisfying assignments. Thus, if we could decide whether a formula has a unique satisfying assignment, we could decide unsatisfiability: $\psi$ has zero satisfying assignments if and only if there is not exactly one satisfying assignment.

Therefore, the problem is at least as hard as UNSAT, so it is coNP-hard.

### 2. Is the problem NP-hard?

Yes, the problem is also NP-hard.

Deciding if $\varphi$ has a unique satisfying assignment is at least as hard as deciding if it has any satisfying assignment (SAT is NP-complete). If we could decide uniqueness, we could decide satisfiability.

