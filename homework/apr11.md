A concrete example of a problem that is both NP-hard and coNP-hard is the problem of deciding whether a Boolean formula is a tautology:

$\text{TAUT} = \{\varphi \mid \varphi \text{ is a Boolean formula that evaluates to true under all assignments}\}$

TAUT is coNP-complete because its complement is SAT, which is NP-complete.

TAUT is NP-hard because for any language $L$ in NP, there is a polynomial-time reduction from $L$ to SAT. For any $x$, one can construct a formula $\varphi_x$ such that $x \in L$ if and only if $\varphi_x$ is satisfiable. Then $x \notin L$ if and only if $\varphi_x$ is unsatisfiable, which is equivalent to $\neg\varphi_x$ being a tautology. Hence, there is a polynomial-time reduction from $L$ to TAUT.

So, TAUT is both NP-hard and coNP-hard.