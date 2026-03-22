Consider the problem of universality for context-free languages: given a context-free grammar $G$ over alphabet $\Sigma$, does $L(G) = \Sigma^*$? This problem is known to be undecidable.

We can use this to show that the equivalence problem for Turing machines is undecidable. The equivalence problem is: given two Turing machines $M_1$ and $M_2$, is $L(M_1) = L(M_2)$?

**Reduction:** Suppose for contradiction that we could decide equivalence of Turing machines. Then, given any context-free grammar $G$ over $\Sigma$, construct:
- $M_1$: a Turing machine that accepts $L(G)$ (possible since Turing machines can accept all recursively enumerable languages, and context-free languages are a strict subclass).
- $M_2$: a Turing machine that accepts $\Sigma^*$ (i.e., on any input, accepts).

Then, $L(G) = \Sigma^*$ if and only if $L(M_1) = L(M_2)$. Thus, if we could decide equivalence of Turing machines, we could decide universality for CFGs, which is impossible.
