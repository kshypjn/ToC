Suppose $f$ is a time-constructible function, that is, we can compute $f(n)$ in $O(f(n))$ time and $f(n) \geq n$.

Claim: If $\mathrm{NTIME}(n) = \mathrm{DTIME}(n)$, then $\mathrm{NTIME}(f(n)) = \mathrm{DTIME}(f(n))$.

Proof:

Suppose $L \in \mathrm{NTIME}(f(n))$. That is, there is a nondeterministic Turing machine $M$ deciding $L$ in time $f(n)$.

We will show $L \in \mathrm{DTIME}(f(n))$ under the assumption $\mathrm{NTIME}(n) = \mathrm{DTIME}(n)$.

Key idea: Simulate $M$ "step-by-step" by reducing the computation to a problem in $\mathrm{NTIME}(n)$.

Construct the following universal verifier $V$:

Given input $x$ of length $n$, guess a computation path of $M$ on $x$ of length at most $f(n)$ (since $M$ runs in time $f(n)$). Encode this computation as a string $w$ of length $O(f(n))$.

Define the language:

$$
L' = \{ (x, w) \mid w \text{ encodes an accepting computation of } M \text{ on } x \text{ in } \leq f(n) \text{ steps} \}
$$

Given $(x, w)$, $L'$ can be decided by a deterministic Turing machine in $O(f(n))$ time, since $M$ is known and $f(n)$ is time-constructible.

Let $L'' = \{ x \mid \exists w,~(x, w) \in L' \}$.

That is, $L''$ is in $\mathrm{NTIME}(f(n))$, and since $\mathrm{NTIME}(n) = \mathrm{DTIME}(n)$, we can derandomize (or simulate nondeterminism) at each step of the computation, provided we have the same amount of time.

But $L'$ is a verification problem; you can reduce $L$ to the acceptance question of some language in $\mathrm{NTIME}(n)$ via padding/trimming construction (since $f(n) \geq n$), or, more directly, note that your simulation at each nondeterministic step can be converted to a deterministic step with the same asymptotic time, since by hypothesis this is possible for all linear-time ($n$) machines.

Thus, one can simulate $M$ deterministically in $O(f(n))$ time, so $L \in \mathrm{DTIME}(f(n))$.

Therefore:
$$
\mathrm{NTIME}(f(n)) = \mathrm{DTIME}(f(n))
$$

Is the converse true?

No, the converse is not necessarily true.

If $\mathrm{NTIME}(f(n)) = \mathrm{DTIME}(f(n))$ for a particular time-constructible function $f(n) \geq n$, this does not generally imply $\mathrm{NTIME}(n) = \mathrm{DTIME}(n)$ for $n$ (i.e., at the linear time bound), since it holds only for $f(n)$ and not potentially for all smaller (e.g., linear) bounds.

For example, you could have separation at linear time (i.e., $\mathrm{NTIME}(n) \neq \mathrm{DTIME}(n)$), but equality at $f(n)$ for some $f(n)\gg n$ due to specific technical properties at higher time bounds.
