To show that $P^{SAT}$ contains both $NP$ and $co\text{-}NP$:

Recall: $P^{SAT}$ is the class of languages decidable in polynomial time by a Turing machine with access to a SAT oracle.

1. $NP \subseteq P^{SAT}$:

NP is the set of languages where membership can be verified efficiently with a witness. SAT is NP-complete, meaning every language in NP can be reduced to SAT in polynomial time.

- For any $L \in NP$, there is a polynomial-time Turing reduction from $L$ to SAT:
    - On input $x$, a polynomial-time machine computes a formula $\phi_x$ such that $x \in L \iff \phi_x$ is satisfiable.
    - A $P^{SAT}$ machine can compute $\phi_x$ and query the SAT oracle on $\phi_x$, deciding $x \in L$ in polynomial time using the oracle.
- Thus, every language in NP can be decided by a polynomial-time machine with SAT oracle access.

2. $co\text{-}NP \subseteq P^{SAT}$:

$co$-$NP$ is the set of languages whose complements are in NP. For $L \in co$-$NP$, $\overline{L} \in NP$. So, deciding $x \in L$ is equivalent to checking $x \notin \overline{L}$.

- By the above, $\overline{L}$ is polynomial-time Turing reducible to SAT; i.e., there is a polynomial-time function mapping $x$ to a Boolean formula $\phi_x$ such that $x \in \overline{L} \iff \phi_x \in SAT$.
- So, $x \in L \iff \phi_x \notin SAT$.
- A $P^{SAT}$ machine can, in polynomial time, compute $\phi_x$, query the SAT oracle, and invert the answer—accept if SAT answers NO (not satisfiable). This is still polynomial time.

Conclusion:  
Both $NP$ and $co$-$NP$ languages can be decided in polynomial time by a deterministic Turing machine with access to a SAT oracle:
\[
NP \subseteq P^{SAT},\quad co\text{-}NP \subseteq P^{SAT}
\]
So, $P^{SAT}$ contains both $NP$ and $co$-$NP$.