To show that checking equivalence of regular expressions is PSPACE-complete, we show two things:
1. The problem is PSPACE-hard.
2. The problem is in PSPACE.

Let the problem be: given two regular expressions $R_1$ and $R_2$ over alphabet $\Sigma$, decide if $L(R_1) = L(R_2)$.

PSPACE-hardness:

It is known that NFA equivalence is PSPACE-complete. Any regular expression can be converted to an equivalent NFA in polynomial time. Given two NFAs, we can convert them to regular expressions, so checking if two regular expressions are equivalent is at least as hard as checking if two NFAs are equivalent. Therefore, the problem is PSPACE-hard.

PSPACE-membership:

Given two regular expressions $R_1$ and $R_2$, we can convert them to NFAs $A_1$ and $A_2$ in polynomial time. To check if $L(R_1) = L(R_2)$, we check if $L(A_1) = L(A_2)$. Checking equivalence of NFAs can be done in PSPACE: guess a string $w$ (of length up to exponential), simulate both NFAs on $w$ using polynomial space, and accept if $w$ is accepted by exactly one of them. By Savitch's theorem, this is in PSPACE.

Therefore, checking equivalence of regular expressions is PSPACE-complete.