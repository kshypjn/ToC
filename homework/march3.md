## step 1
now, the set of all finite binary strings is $\{0,1\}^*$, and this set is countably infinite.listing them in order:

$$\epsilon, 0, 1, 00, 01, 10, 11, 000, \ldots$$

since every TM corresponds to at least one finite string encoding, and the set of finite strings is countable, the set of all Turing machines is also countable. formally:

$$|\{\text{Turing machines}\}| = \mathbb{N}$$

so we can write all TMs as a list $M_1, M_2, M_3, \ldots$

---

## step 2: there are uncountably many languages

let $\Sigma = \{0, 1\}$ (or any finite alphabet with at least one symbol). then $\Sigma^*$ is the set of all finite strings over $\Sigma$, which is countably infinite — same argument as above, just list them.

now, a language is just a subset $L \subseteq \Sigma^*$. so the set of all languages is the power set $\mathcal{P}(\Sigma^*)$.

from Cantor's theorem that for any set $S$:

$$|\mathcal{P}(S)| > |S|$$

since $\Sigma^*$ is countably infinite, its power set is uncountably infinite. more precisely, since $\Sigma^*$ is countable we can write $\Sigma^* = \{s_1, s_2, s_3, \ldots\}$, and then each language $L$ corresponds to an infinite binary sequence (the characteristic sequence):

$$\chi_L = (b_1, b_2, b_3, \ldots) \quad \text{where } b_i = 1 \iff s_i \in L$$

the set of all such infinite binary sequences is $\{0,1\}^{\mathbb{N}}$, and by Cantor's diagonal argument this set is uncountable. so:

$$|\mathcal{P}(\Sigma^*)| = |\{0,1\}^{\mathbb{N}}| = 2^{\mathbb{N}} > \mathbb{N}$$

---

## step 3: the diagonal argument 

listing all infinite binary sequences:

$$r_1 = b_{11} b_{12} b_{13} \ldots$$
$$r_2 = b_{21} b_{22} b_{23} \ldots$$
$$r_3 = b_{31} b_{32} b_{33} \ldots$$

now define a new sequence $d$ by flipping the diagonal:

$$d_i = 1 - b_{ii}$$

then $d$ differs from every $r_i$ in at least the $i$-th position, so $d$ is not in the list. contradiction. so no such listing exists and $\{0,1\}^{\mathbb{N}}$ is uncountable.

---

each Turing machine $M$ recognizes exactly one language $L(M) \subseteq \Sigma^*$. so the set of recursively enumerable (RE) languages has size at most the number of Turing machines, which is countable:

$$|\{\text{RE languages}\}| \leq |\{\text{Turing machines}\}| = \mathbb{N}$$

but the set of all languages has size $2^{\mathbb{N}}$, which is strictly greater:

$$|\{\text{all languages}\}| = 2^{\mathbb{N}} > \mathbb{N}$$

so there are strictly more languages than there are Turing machines. this means:

$$|\{\text{all languages}\}| - |\{\text{RE languages}\}| \neq 0$$



