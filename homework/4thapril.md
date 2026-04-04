The NFA intersection problem is: given two NFAs $A_1$ and $A_2$, decide whether $L(A_1) \cap L(A_2) \neq \emptyset$.

Given $A_1 = (Q_1, \Sigma, \delta_1, q_{1,0}, F_1)$ and $A_2 = (Q_2, \Sigma, \delta_2, q_{2,0}, F_2)$, we can construct a product NFA $A = (Q, \Sigma, \delta, q_0, F)$ as follows:

- $Q = Q_1 \times Q_2$
- $q_0 = (q_{1,0}, q_{2,0})$
- For each $(q_1, q_2) \in Q$ and $a \in \Sigma$:
    - $\delta((q_1, q_2), a) = \{(q_1', q_2') \mid q_1' \in \delta_1(q_1, a),\ q_2' \in \delta_2(q_2, a)\}$
- $F = F_1 \times F_2$

The language $L(A) = L(A_1) \cap L(A_2)$ is nonempty if and only if there exists a path from $q_0$ to some $(f_1, f_2) \in F$. To check this, we can perform a breadth-first search (BFS) starting from $q_0$ over the state space of $A$. If we reach a state in $F$, then $L(A) \neq \emptyset$.

The number of states in the product automaton is $|Q_1| \times |Q_2|$, and the BFS runs in time polynomial in the sizes of $A_1$ and $A_2$.

Therefore, the NFA intersection problem is in $P$.