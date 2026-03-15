For a fixed $M$ and $w$, let $Val_{M,w}$ be the set of strings that encode valid accepting computation histories of $M$ on $w$. It is a standard fact that the complement $\overline{Val_{M,w}}$ is context-free: we can build a CFG $G$ such that $L(G) = \overline{Val_{M,w}}$ (for example, by taking the union of context-free languages that each capture one type of “invalid” string—wrong format, wrong initial configuration, wrong transition, or non-accepting).

So from any pair $(M, w)$ we can effectively construct a CFG $G$ with $L(G) = \overline{Val_{M,w}}$.

If $M$ does not accept $w$, then $Val_{M,w} = \emptyset$, so $L(G) = \overline{\emptyset} = \Sigma^*$, which is regular.

If $M$ accepts $w$, then $Val_{M,w}$ is nonempty. In that case, $Val_{M,w}$ is not a regular language: its strings have the form $C_1$ \texttt{\#} $C_2$ \texttt{\#} $\cdots$ \texttt{\#} $C_k$ with constraints that link the contents of consecutive configurations (each $C_{i+1}$ must be the unique successor of $C_i$). That kind of linked structure cannot be recognized by a finite automaton. So when $Val_{M,w}$ is nonempty, it is not regular. Regular languages are closed under complement, so $\overline{Val_{M,w}}$ is not regular either when $Val_{M,w}$ is nonempty. Hence when $M$ accepts $w$, $L(G) = \overline{Val_{M,w}}$ is not regular.

So $L(G)$ is regular if and only if $M$ does not accept $w$. If we had an algorithm to decide whether a given CFG generates a regular language, we could decide whether $M$ does not accept $w$, and by negating the answer we would decide whether $M$ accepts $w$. That would make the acceptance problem decidable, which is false. So the problem of checking whether a context-free grammar generates a regular language is undecidable.
