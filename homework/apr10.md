A sorting network is a fixed sequence of compare-exchange operations that is supposed to sort any input of $n$ values (typically 0-1 inputs).

Given a sorting network $N$, the validity problem is: Does $N$ correctly sort all possible inputs?

1. The problem is in coNP:

The complement problem is: Is there an input $x$ such that $N(x)$ is not sorted? This is in NP: a certificate is such an $x$, and given $x$ we can efficiently simulate $N$ and check if the output is not sorted. Therefore, validity is in coNP.

2. The problem is coNP-hard:

We can reduce from the UNSAT problem, which is coNP-complete. Given a Boolean formula $\varphi(x_1, \dots, x_n)$, we can construct a sorting network $N_\varphi$ (in polynomial time) that sorts all inputs if and only if $\varphi$ is unsatisfiable. If $\varphi$ is satisfiable, there is some assignment making the output not sorted. If it is unsatisfiable, all possible inputs are sorted. Thus, validity is at least as hard as UNSAT.

Therefore, checking if a given sorting network is valid is coNP-complete.