The 2-CNF-SAT problem is: Given a Boolean formula in conjunctive normal form, where each clause has at most 2 literals (i.e., is of the form $(x \vee y)$, $(x \vee \neg y)$, etc.), decide whether the formula is satisfiable.

We now prove that 2-CNF-SAT can be solved in polynomial time.

1. Reduction to Implication Graph:

Every 2-CNF formula can be written as a conjunction of clauses, each of the form $(\ell_1 \vee \ell_2)$, where $\ell_1$ and $\ell_2$ are literals (variables or their negations). Observe that
$(\ell_1 \vee \ell_2) \equiv (\neg \ell_1 \rightarrow \ell_2) \wedge (\neg \ell_2 \rightarrow \ell_1)$.

Construct a directed graph $G$ called the implication graph as follows:
- The vertices are all literals ($x_1, \ldots, x_n, \neg x_1, \ldots, \neg x_n$).
- For each clause $(\ell_1 \vee \ell_2)$, add edges $(\neg \ell_1 \rightarrow \ell_2)$ and $(\neg \ell_2 \rightarrow \ell_1)$.

2. Satisfiability Condition:

The formula is unsatisfiable if there exists some variable $x$ such that both $x$ and $\neg x$ are mutually reachable in $G$ (i.e., $x$ and $\neg x$ are in the same strongly connected component).

Proof: If $x$ and $\neg x$ are in the same SCC, assigning $x = \text{True}$ implies $x = \text{False}$ (and vice versa), which is impossible.

Otherwise, the formula is satisfiable. An explicit assignment can be constructed as follows:
- Compute strongly connected components.
- Topologically order the SCCs.
- For each variable $x$:
    - If $x$'s SCC comes before $\neg x$'s SCC, assign $x = \text{False}$.
    - Else, assign $x = \text{True}$.

3. Algorithm and Running Time:

- Build the implication graph: $O(n + m)$ time, where $n$ is the number of variables and $m$ is the number of clauses.
- Find strongly connected components (e.g., Kosaraju's algorithm): $O(n + m)$ time.
- Assign values as described above: $O(n)$ time.

Thus, the entire algorithm runs in polynomial time.

Conclusion: 2-CNF-SAT is in $P$ because it can be reduced to checking SCCs in the implication graph, which is solvable in polynomial time.