To prove that the $k$-Colorability problem is NP-complete (for $k \geq 3$), we need to show two things:

1. **$k$-Colorability is in NP**:  
Given a graph $G = (V, E)$ and a certificate (an assignment of $k$ colors to the vertices), we can verify in polynomial time whether this coloring is valid:
   - For each edge $(u, v) \in E$, check that the color assigned to $u$ is different from the color assigned to $v$.
   - This requires checking all $|E|$ edges, each check taking constant time, so overall this is polynomial.

2. **$k$-Colorability is NP-hard**:  
We show this by giving a reduction from a known NP-complete problem to $k$-Colorability. The standard reduction is from 3-Colorability to $k$-Colorability (for $k > 3$), but to prove NP-hardness for $k=3$, we usually reduce from 3-SAT, a well-known NP-complete problem.

**Reduction from 3-SAT to 3-Colorability**:

Given a 3-SAT instance with variables $x_1, ..., x_n$ and clauses $C_1, ..., C_m$, we construct a graph $G$ that is 3-colorable if and only if the formula is satisfiable. The high-level idea:
- We create a "color triangle" with three vertices: $T$ (True), $F$ (False), and $B$ (Base), all connected to each other. These enforce that their colors are different and fix three global colors for the construction.
- For each variable $x_i$, add a vertex $v_{x_i}$ and a vertex $v_{\bar{x}_i}$. Connect both to each other and to $B$; this ensures that in any coloring, one is colored $T$ and the other $F$, and neither is $B$.
- For each clause, create a clause gadget: add a triangle of vertices, each corresponding to one literal of the clause. Connect each such literal vertex to the corresponding variable/literal vertex.
- The construction ensures that the graph can be properly 3-colored if and only if there is an assignment to the variables making all clauses true (i.e., a satisfying assignment).

Building this graph from a 3-SAT instance can be done in polynomial time.

Thus, $k$-Colorability (for $k \geq 3$) is NP-hard.

