## Intersection of a Regular Language and a Context-Free Language

Let $R$ be a regular language over alphabet $\Sigma$, recognized by a DFA
$M_R = (Q_R, \Sigma, \delta_R, q_{0,R}, F_R)$, and let $C$ be a context-free language over $\Sigma$, recognized by a PDA
$M_C = (Q_C, \Sigma, \Gamma, \delta_C, q_{0,C}, Z_0, F_C)$.

We construct a new PDA $M$ that recognizes $R \cap C$:

- States: $Q = Q_R \times Q_C$.
- Input alphabet: $\Sigma$.
- Stack alphabet: $\Gamma$ (same as $M_C$).
- Start state: $(q_{0,R}, q_{0,C})$, with initial stack symbol $Z_0$.
- Transitions:
  - Whenever $M_C$ has a move $\delta_C(q_C, a, X) \ni (q_C', \alpha)$ (read symbol $a$, pop $X$, push $\alpha$),
  - and the DFA has move $\delta_R(q_R, a) = q_R'$,
  - define $M$’s move from $(q_R, q_C)$ on input $a$ and stack top $X$ to $(q_R', q_C')$ with the same stack behavior $\alpha$.
  - For $\varepsilon$-moves of the PDA, keep the DFA component unchanged.
- Accepting states: $F = \{(q_R, q_C) \mid q_R \in F_R,\ q_C \in F_C\}$.

Thus $M$ simulates the DFA for $R$ and the PDA for $C$ in parallel, and accepts exactly the strings accepted by both. Therefore, $R \cap C$ is context-free.

---

## Intersection of Two Context-Free Languages Need Not Be Context-Free

Consider alphabet $\{a,b,c\}$ and the following languages:

- $L_1 = \{ a^i b^i c^j \mid i,j \ge 0 \}$.

  A context-free grammar for $L_1$ is:
  - $S \to aSb \mid T$
  - $T \to cT \mid \varepsilon$

- $L_2 = \{ a^i b^j c^j \mid i,j \ge 0 \}$.

  A context-free grammar for $L_2$ is:
  - $S \to A T$
  - $A \to aA \mid \varepsilon$
  - $T \to bTc \mid \varepsilon$

Any string in $L_1$ has equal numbers of $a$’s and $b$’s (say $n$) followed by any number of $c$’s. Any string in $L_2$ has any number of $a$’s followed by equal numbers of $b$’s and $c$’s (say $n$). So a string lies in both $L_1$ and $L_2$ iff it has the same number of $a$’s, $b$’s, and $c$’s:

$$
L_1 \cap L_2 = \{ a^n b^n c^n \mid n \ge 0 \}.
$$

 Hence, although $L_1$ and $L_2$ are context-free, their intersection is not.

Therefore, the class of context-free languages is not closed under intersection.

