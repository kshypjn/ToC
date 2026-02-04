If $L$ is regular, then $\downarrow L$ is regular.

Since $L$ is regular, there exists a DFA $M = (Q, \Sigma, \delta, q_0, F)$ that recognizes $L$.

constructing a NFA $N$ that recognizes $\downarrow L$.

for words $w, u \in \Sigma^*$, we have $w \leq u$ if:
1. $w = u$, or
2. $w$ is a proper prefix of $u$, or  
3. $w = xav$ and $u = xbv'$ where $x \in \Sigma^*$ is the longest common prefix, 
   $a, b \in \Sigma$ with $a < b$, and $v, v' \in \Sigma^*$

Construction of NFA for $\downarrow L$

an NFA $N = (Q', \Sigma, \delta', q'_0, F')$ where:

**States**: 
$$Q' = Q \times \{0, 1\}$$

The second component is a flag indicating:
- $0$: we are following a path equal to some word in $L$ (same prefix till now)
- $1$: it has already chosen a lexicographically smaller symbol

**Initial state**: 
$$q'_0 = (q_0, 0)$$

**Transition function** $\delta'$:

For state $(q, f) \in Q'$ and symbol $a \in \Sigma$:

1. Continuing equal (from flag $0$ to flag $0$):
   $$(q, 0) \xrightarrow{a} (\delta(q, a), 0)$$

2.
   For each $b \in \Sigma$ with $b > a$, if there exists a path in $M$ from $\delta(q, b)$ 
   to some accepting state in $F$, then:
   $$(q, 0) \xrightarrow{a} (\delta(q, a), 1)$$

3.
   For any $q' \in Q$:
   $$(q, 1) \xrightarrow{a} (q', 1)$$

**Accepting states**:
$$F' = \{(q, 0) : q \in F\} \cup \{(q, 1) : q \in Q\}$$

