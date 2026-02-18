constructing a standard DFA $M'$ that simulates $M$ step-by-step.
$$M = (Q,\, \Sigma,\, \Gamma,\, k,\, \delta,\, q_0,\, A_0,\, F)$$
Define:

$$M' \;=\; (Q',\; \Sigma,\; \delta',\; q_0',\; F')$$

with components:

| Component | Definition |
|-----------|------------|
| $Q'$ | $Q \times \Gamma^k$ |
| $q_0'$ | $(q_0,\, A_0)$ |
| $\delta'\bigl((q,A),\,a\bigr)$ | $(q',A')$ where $(q',A') = \delta(q,\,a,\,A)$ |


$M'$ is a valid DFA because $|Q'| = |Q| \cdot |\Gamma|^k < \infty$.

---

Correctness: $L(M') = L(M)$

Claim :  For every input $w = a_1 a_2 \cdots a_n$ and every $0 \le i \le n$, if $(q_i, A_i)$ is the configuration of $M$ after reading $a_1 \cdots a_i$, then the state of $M'$ after reading the same prefix is $(q_i, A_i)$.

Proof by induction on $i$

- **Base case ($i = 0$):** The initial state of $M'$ is $(q_0, A_0)$, which matches the initial configuration of $M$. 

- **Inductive step:** Assume the state of $M'$ after reading $a_1 \cdots a_i$ is $(q_i, A_i)$. On reading $a_{i+1}$:

$$\delta'\bigl((q_i, A_i),\; a_{i+1}\bigr) \;=\; (q_{i+1}, A_{i+1})$$

where $(q_{i+1}, A_{i+1}) = \delta(q_i,\, a_{i+1},\, A_i)$, which is exactly how $M$ transitions. 

**Acceptance equivalence.** After reading all of $w$, $M'$ is in state $(q_n, A_n)$. By definition of $F'$:

$$(q_n, A_n) \in F' \iff q_n \in F$$

Therefore $M'$ accepts $w$ if and only if $M$ accepts $w$, so $L(M') = L(M)$.

