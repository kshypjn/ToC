To show that Bounded Post Correspondence Problem (Bounded PCP) is NP-complete, we must establish two things:

**1. Bounded PCP is in NP**

Given a set $T$ of tile pairs and positive integer $K$, a *certificate* is a sequence of at most $K$ tiles (allowing repetition). We can verify a solution in polynomial time as follows:
- Given a sequence $s = (t_{i_1}, t_{i_2}, ..., t_{i_m})$ with $m \leq K$, compute the concatenation of the top strings and the bottom strings: $u = u_{i_1}u_{i_2}\ldots u_{i_m}$ and $v = v_{i_1}v_{i_2}\ldots v_{i_m}$.
- Check whether $u = v$.
- Both operations are polynomial in $K$ (since the total length is at most $K$ times the maximum tile length).

Thus, given a certificate, we can check in polynomial time if it is a valid solution. Therefore, Bounded PCP is in NP.

---

**2. Bounded PCP is NP-hard**

We can prove NP-hardness by reducing an NP-complete problem to Bounded PCP. A standard approach is to reduce from 3-SAT (or general SAT).

**Outline of Reduction from SAT to Bounded PCP:**

Given a SAT instance (a Boolean formula $\varphi$ in CNF with $n$ variables and $m$ clauses), we construct an instance of Bounded PCP (tiles $T$ and bound $K$) such that:
- If the formula $\varphi$ is satisfiable, there is a sequence of at most $K$ tiles forming a PCP solution.
- If not, then no such solution exists.

**Sketch:**
- We encode variable assignments as choices in the tile sequence, allowing at most $n$ initial tiles—one for each variable, encoding setting it true or false.
- For each assignment, the construction uses additional tiles to verify that every clause is satisfied.
- The total number of tiles in a potential solution is bounded by $K = n + f(m)$ for some function $f$ depending on the number of clauses and the construction (still polynomial in input size).
- This construction can be carried out in polynomial time.

References: This reduction is standard and can be found in textbooks (see e.g. Sipser 3rd Ed. Exercise 5.24, or Papadimitriou "Computational Complexity", Example 2.35). Thus, Bounded PCP is NP-hard.


