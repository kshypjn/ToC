# Recursively enumerable languages are closed under quotient

The quotient of two languages $L_1$ and $L_2$ is
$L_1 / L_2 = \{ x \mid \exists y \in L_2 \text{ such that } xy \in L_1 \}$.

Assume $L_1$ and $L_2$ are recursively enumerable. So there exist Turing machines $M_1$ and $M_2$ that semi-decide $L_1$ and $L_2$: $M_1$ accepts exactly the strings in $L_1$ (and may loop on strings not in $L_1$), and $M_2$ accepts exactly the strings in $L_2$.

We build a Turing machine $M$ that semi-decides $L_1 / L_2$.

$M$ on input $x$:
1. Enumerate all strings $y$ over the alphabet in a canonical order (e.g. by length, then lexicographically: $\varepsilon$, $a$, $b$, $aa$, $ab$, …).
2. For each $y$, run $M_1$ on $xy$ and $M_2$ on $y$. To avoid infinite loops when one of them loops, dovetail: simulate one step of $M_1(xy)$, then one step of $M_2(y)$, then two steps of each, and so on, so that if either ever halts we eventually see it.
3. If for some $y$ both $M_1$ accepts $xy$ and $M_2$ accepts $y$, then halt and accept $x$.

If $x \in L_1 / L_2$, then there is some $y \in L_2$ with $xy \in L_1$. For that $y$, both $M_1(xy)$ and $M_2(y)$ eventually accept, so $M$ will accept $x$. If $x \notin L_1 / L_2$, then for every $y$, either $xy \notin L_1$ or $y \notin L_2$, so $M$ never finds a $y$ with both accepting; $M$ runs forever. So $M$ semi-decides $L_1 / L_2$, and $L_1 / L_2$ is recursively enumerable.

Hence RE languages are closed under quotient.
