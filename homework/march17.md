
Take the alphabet $\Sigma = \{a\}$. So every string is of the form $a^n$ for some $n \geq 0$.

We encode natural numbers by length: $n$ is represented by the string $a^n$. Fix a standard listing of all Turing machines $M_0, M_1, M_2, \ldots$ (e.g. by encoding TMs as strings and ordering by length, then lexicographically).

Define
$K = \{ i \in \mathbb{N} \mid M_i \text{ halts on input } \epsilon \}$
This is the halting set: the set of indices of TMs that halt on the empty string. It is a standard result that $K$ is undecidable.

Define the language over $\Sigma$:
$L = \{ a^i \mid i \in K \} = \{ a^i \mid M_i \text{ halts on } \epsilon \}$

$L$ is a language over the singleton alphabet $\{a\}$.

If $L$ were recursive, we could decide membership in $K$ as follows: on input $i$, build the string $a^i$, run the decider for $L$ on $a^i$, and say $i \in K$ iff the decider accepts. So $K$ would be decidable, which is false. Hence $L$ is not recursive.

So $L = \{ a^i \mid M_i \text{ halts on } \epsilon \}$ is an example of a language over the singleton alphabet $\{a\}$ that is not recursive.
