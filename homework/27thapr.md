To show that $SPACE(n) \neq NP$, we use the space hierarchy theorem and properties of NP.

1. $SPACE(n)$: The set of decision problems solvable by a deterministic Turing machine using $O(n)$ space.
2. $NP$: The class of decision problems solvable by a nondeterministic Turing machine in polynomial time.



The Space Hierarchy Theorem states that for any space-constructible function $f(n)$, there are languages that can be decided in $O(f(n))$ space but not in $o(f(n))$ space. In particular:
- $SPACE(n) \subset SPACE(n^2)$ (the containment is strict)



$PSPACE$ is the class of problems solvable in polynomial space (possibly exponential time).
$NP \subseteq PSPACE$ because any problem that can be solved nondeterministically in polynomial time can also be solved deterministically in polynomial space (by exploring the whole computation tree in polynomial space).

But also, for any polynomial $p(n)$, $NP \subseteq SPACE(p(n))$.
In particular, $NP \subseteq SPACE(n^k)$ for some $k$.



From the space hierarchy theorem, $SPACE(n)$ is strictly smaller than $PSPACE$ since $PSPACE = \bigcup_k SPACE(n^k)$.
There are languages in $SPACE(n^2)$ that are not in $SPACE(n)$, by the hierarchy theorem.


If $SPACE(n) = NP$, then we would have $NP \subseteq SPACE(n) \subseteq PSPACE$, but
since $NP$ contains problems believed to require more than linear space (for example, some $PSPACE$-complete problems need polynomial space), and the strict inclusion from the hierarchy theorem, this is not possible.

Therefore, since $NP \subseteq PSPACE$, and $SPACE(n) \subset PSPACE$ (and this containment is strict), there must be languages in $NP$ which are not in $SPACE(n)$. Hence,

$SPACE(n) \neq NP$
