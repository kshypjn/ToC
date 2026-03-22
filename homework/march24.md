To determine whether the language $L = \{\langle M, w, n \rangle \mid M \text{ halts on } w \text{ in at most } 2^n \text{ steps}\}$ is decidable, let's analyze the problem:

A Turing machine $M$, input $w$, and integer $n$ are given; the question is whether, when $M$ is started on $w$, it halts within at most $2^n$ steps.

**Proof that $L$ is Decidable:**

We can construct a decider $D$ for $L$, which, on input $\langle M, w, n \rangle$:

1. Simulates $M$ on $w$ for at most $2^n$ steps.
2. If $M$ halts within those $2^n$ steps, $D$ accepts.
3. If $M$ does not halt within $2^n$ steps (i.e., the simulation reaches step $2^n$ and $M$ has not halted), $D$ rejects.

This is a standard bounded time simulation and is entirely computable: for any particular $n$, $2^n$ is some finite number, and a Turing machine can simulate another for a bounded number of steps. Thus, such a decider always halts.

Therefore, **membership in $L$ is decidable**.