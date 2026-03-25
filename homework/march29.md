Suppose, for contradiction, that $g(n)$ is a computable function. That is, for any $n$, we can compute the maximum length $g(n)$ such that it suffices to check all solutions to any $n$-tile binary PCP instance up to that length.

Given any set $T$ of $n$ binary tiles, we could compute $g(n)$. Then, we could systematically check all possible sequences of tiles of length at most $g(n)$ to see if any of them form a solution for $T$ (i.e., whether the top and bottom strings match when the tiles are concatenated in that order). Since there are only finitely many such sequences (specifically, at most $n^{g(n)}$), this process would let us decide whether $T$ has a solution: if we find a matching sequence, then $T$ is solvable; if not, it is unsolvable.

But the Post Correspondence Problem is known to be undecidable, even when restricted to binary tiles, so there cannot exist an algorithm that decides PCP in general. This is a contradiction.

Therefore, our assumption that $g$ is computable must be false. Thus, $g(n)$ is not a computable function.