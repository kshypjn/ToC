To show the relativized world results regarding $P$ and $NP$, we must construct two oracles, $A$ and $B$, with the following properties:
- For oracle $A$: $P^A = NP^A$  
- For oracle $B$: $P^B \neq NP^B$

### 1. There exists an oracle $A$ such that $P^A = NP^A$.

Proof (outline):

Let $A$ be a $PSPACE$-complete language (for example, the language $TQBF$: the set of true quantified Boolean formulae).

Recall that:
- $P^{TQBF} = PSPACE$
- $NP^{TQBF} = PSPACE$

That is, both deterministic and nondeterministic polynomial-time machines with access to a $PSPACE$-complete oracle can solve anything in $PSPACE$ in polynomial time (since querying a $PSPACE$-complete oracle is "cheap" relative to $PSPACE$). Therefore:

Conclusion:  
There exists an oracle $A$ (e.g., $TQBF$), such that $P^A = NP^A$.

---

### 2. There exists an oracle $B$ such that $P^B \neq NP^B$.

Proof (Baker-Gill-Solovay 1975):

Baker, Gill, and Solovay constructed such an oracle $B$. The idea is to "diagonalize" against all deterministic polynomial-time oracle Turing machines so that there is a language in $NP^B$ that is not in $P^B$. Informally, $B$ is constructed so that $NP^B$ can solve a certain "oracle-encoded" hard language (like a variant of the sparse set), but no deterministic polynomial-time machine can, since for each such machine we can build $B$ adversarially. The full proof involves a priority construction.

