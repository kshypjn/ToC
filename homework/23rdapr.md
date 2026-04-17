Suppose $P = NP$. We want to show $EXP = NEXP$.

Recall: $EXP$ is the class of problems solved by deterministic Turing machines in exponential time. $NEXP$ is the class of problems solved by non-deterministic Turing machines in exponential time.

We always have $EXP \subseteq NEXP$, so it is enough to show $NEXP \subseteq EXP$.

Let $L$ be a language in $NEXP$. There is some non-deterministic machine $M$ and a constant $k$ such that on input $x$, $M$ runs in time $2^{O(n^k)}$ and accepts $x$ if and only if $x \in L$.

Given $x$, consider the question: does $M$ accept $x$ within $2^{n^k}$ steps? This can be reduced to a SAT instance of size polynomial in $2^{n^k}$. (We can encode the computation history as a SAT formula.)

If $P = NP$, then SAT can be solved in polynomial time. But the size of the formula is already exponential in $n$, so with $P = NP$, we can decide $L$ in deterministic exponential time.

Alternatively, using a padding argument: define $L' = \{ x 1^{2^{n^k}} : x \in L \}$. $L'$ is in $NP$, and since $P = NP$, $L'$ can be decided in deterministic polynomial time relative to the input length. But the input is of length exponential in $n$, so this gives an exponential time deterministic algorithm for $L$.

Therefore, $NEXP \subseteq EXP$, so $EXP = NEXP$ if $P = NP$.