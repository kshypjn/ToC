To prove that the Hamiltonian Path problem is NP-complete, we must show two things:

1. **Hamiltonian Path is in NP:**  
Given a graph \( G = (V, E) \) and a sequence of vertices, we can check in polynomial time whether this sequence forms a path that visits every vertex exactly once—i.e., whether it is a Hamiltonian path. This verification can be done by:
   - Checking that the sequence contains each vertex exactly once,
   - Verifying that consecutive vertices in the sequence are connected by an edge in \( E \).
Therefore, Hamiltonian Path is in NP.

2. **Hamiltonian Path is NP-hard:**  
We can show this by reducing a known NP-complete problem to Hamiltonian Path in polynomial time. The standard reduction is from the Hamiltonian Cycle problem, which is known to be NP-complete.

**Reduction from Hamiltonian Cycle to Hamiltonian Path:**  
Given an instance of the Hamiltonian Cycle problem for a graph \( G = (V, E) \), construct a new graph \( G' \) as follows:
- For every edge \( (u, v) \) in \( G \), keep it in \( G' \).
- For every vertex \( v \in V \), add a new vertex \( v' \), and connect \( v' \) to \( v \).
- Pick any vertex \( s \in V \), and let \( s' \) be its added duplicate. Let \( t' \) be the duplicate of another vertex \( t \neq s \).
- Ask if \( G' \) has a Hamiltonian path from \( s' \) to \( t' \).

Alternatively, the reduction can be phrased more simply:  
Given an instance of Hamiltonian Cycle on \( G \), pick any edge \( (u, v) \) in \( G \), and construct \( G' \) by removing that edge. Then, ask whether \( G' \) has a Hamiltonian path from \( u \) to \( v \). \( G \) has a Hamiltonian cycle if and only if \( G' \) has a Hamiltonian path from \( u \) to \( v \).

Since the Hamiltonian Cycle problem is NP-complete, and we can reduce it to the Hamiltonian Path problem in polynomial time, Hamiltonian Path is NP-hard.
