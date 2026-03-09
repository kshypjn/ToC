Let $E_{TM} = \{\langle M \rangle \mid M \text{ is a TM and } L(M) = \emptyset\}$. We want to show that its complement
$
\overline{E_{TM}} = \{\langle M \rangle \mid M \text{ is a TM and } L(M) \neq \emptyset\}
$
is Turing recognizable. We want to build a Turing machine $R$ such that:

- If $L(M) \neq \emptyset$, then $R$ eventually accepts $\langle M \rangle$.
- If $L(M) = \emptyset$, then $R$ never accepts $\langle M \rangle$ (it may run forever).

Idea: $\overline{E_{TM}}$ contains exactly those TMs that accept at least one string. So on input $\langle M \rangle$, we want to systematically search for some string that $M$ accepts. If we ever find such a string, we accept $\langle M \rangle$.

Let $\Sigma$ be the input alphabet of $M$. We can effectively enumerate all strings over $\Sigma$ as
\[
w_1, w_2, w_3, \dots
\]
for example, shortlex order.

Now we define a Turing machine $R$ that recognizes $\overline{E_{TM}}$:

On input $\langle M \rangle$:
1. Enumerate all strings in $\Sigma^*$ as $w_1, w_2, w_3, \dots$.
2. For stages $s = 1, 2, 3, \dots$ do:
   - For each $i = 1, 2, \dots, s$, simulate $M$ on input $w_i$ for one additional step (continuing from where the simulation left off in previous stages).
   - If during any of these simulations, $M$ ever accepts some $w_i$, then $R$ accepts $\langle M \rangle$.

This is a dovetailing procedure where we interleave all computations $M(w_1), M(w_2), \dots$ so that if any of them eventually accepts, we will see it in finite time.


