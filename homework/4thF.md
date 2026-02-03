If $L$ is Regular, then $L^*$ is Regular

 Proof

Regular languages are exactly the languages described by regular expressions.  
The class of regular languages:

- Contains $\emptyset$, $\{\varepsilon\}$, and $\{a\}$ for $a \in \Sigma$
- Is closed under union, concatenation, and Kleene star

If $L$ is regular, then there exists a regular expression $r$ such that

$$
L = L(r).
$$

Applying Kleene star to $r$ gives another regular expression $r^*$. Hence

$$
L(r^*) = (L(r))^* = L^*.
$$

Therefore, $L^*$ is regular.



the Converse is Not True

Counterexample

Let

$$
L = \{ a^{2^n} \mid n \ge 0 \}.
$$

This is the set of strings of $a$’s whose length is a power of $2$.

Claim 1: $L$ is not regular

Assume $L$ is regular with pumping length $p$.

Let

$$
s = a^{2^p} \in L.
$$

By the Pumping Lemma, write

$$
s = xyz
$$

with

- $|xy| \le p$
- $|y| \ge 1$
- $xy^i z \in L$ for all $i \ge 0$

Let $|y| = k \ge 1$.

Pump down ($i=0$):

$$
|xy^0 z| = 2^p - k.
$$

But

$$
2^{p-1} < 2^p - k < 2^p,
$$

so $2^p - k$ lies strictly between two powers of $2$, hence is not a power of $2$.

Contradiction. Therefore $L$ is not regular.

Claim 2: $L^*$ is regular

Every string in $L$ consists only of $a$’s, so

$$
L^* \subseteq a^*.
$$

Now show $a^* \subseteq L^*$.

Any integer $n \ge 1$ has a binary representation:

$$
n = 2^{i_1} + 2^{i_2} + \cdots + 2^{i_k}.
$$

Thus

$$
a^n = a^{2^{i_1}} a^{2^{i_2}} \cdots a^{2^{i_k}}.
$$

Each factor is in $L$, so $a^n \in L^*$.

Also $\varepsilon \in L^*$.

Therefore

$$
L^* = a^*,
$$

which is regular.



