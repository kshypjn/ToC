

Let
$L = \{\langle p,c\rangle \mid c \text{ is the caste of the person } p\}.$

To make this a formal language decision problem, we interpret:

- $p$ as the encoding $\langle P\rangle$ of a Turing machine/program $P$ (a "person").
- $c$ as a symbol from a fixed finite set of caste labels, e.g. $\{B,S\}$ (think "Brahmin" and "Shudra").

Now define the "caste of a person/program" by a precise mathematical rule:

$\mathrm{caste}(P)=
\begin{cases}
B & \text{if } P \text{ halts on empty input } \epsilon \\
S & \text{if } P \text{ does not halt on empty input } \epsilon
\end{cases}
$

Then the language becomes
$L = \{\langle \langle P\rangle, c\rangle \mid c = \mathrm{caste}(P)\}.$

We will show that deciding membership in $L$ is undecidable by reducing the Halting Problem to it.



Let
$HALT_\epsilon = \{\langle P\rangle \mid P \text{ halts on input } \epsilon\}.$
It is a standard result that $HALT_\epsilon$ is undecidable.


Assume for contradiction that $L$ is decidable. Then there exists a decider $D_L$ such that for every pair $\langle \langle P\rangle, c\rangle$:

- $D_L$ accepts iff $\langle \langle P\rangle, c\rangle \in L$.
- $D_L$ rejects otherwise.

Using $D_L$, construct a decider $D_H$ for $HALT_\epsilon$:

Machine $D_H$ on input $\langle P\rangle$:

1. Run $D_L$ on input $\langle \langle P\rangle, B\rangle$.
2. If $D_L$ accepts, then accept.
3. If $D_L$ rejects, then reject.


Fix any program $P$.

- If $P$ halts on $\epsilon$, then by definition $\mathrm{caste}(P) = B$, so $\langle \langle P\rangle, B\rangle \in L$. Therefore $D_L$ accepts, so $D_H$ accepts.
- If $P$ does not halt on $\epsilon$, then $\mathrm{caste}(P) = S$, so $\langle \langle P\rangle, B\rangle \notin L$. Therefore $D_L$ rejects, so $D_H$ rejects.

Thus $D_H$ decides $HALT_\epsilon$.

