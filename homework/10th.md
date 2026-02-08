Constructing a weighted automaton over $\mathbb{R}$ with alphabet $\Sigma = \{a\}$ that computes $f(a^n) = n$.

The weight of a run $\rho = q_0 \xrightarrow{a_1} q_1 \xrightarrow{a_2} \cdots \xrightarrow{a_n} q_n$ is:

$$\text{weight}(\rho) = \lambda(q_0) \cdot \mu(q_0, a_1, q_1) \cdot \mu(q_1, a_2, q_2) \cdots \mu(q_{n-1}, a_n, q_n) \cdot \gamma(q_n)$$

The weight of a word $w$ is the sum over all runs:

$$[\![A]\!](w) = \sum_{\rho \text{ run on } w} \text{weight}(\rho)$$

### Construction

States: $Q = \{q_0, q_1\}$

Initial weights:
- $\lambda(q_0) = 1$
- $\lambda(q_1) = 0$

Transition weights:
- $\mu(q_0, a, q_0) = 1$
- $\mu(q_0, a, q_1) = 1$
- $\mu(q_1, a, q_1) = 1$
- All other transitions have weight $0$

Final weights:
- $\gamma(q_0) = 0$
- $\gamma(q_1) = 1$


Correctness - Check

For input $a^n$, consider all runs from $q_0$ to $q_1$. A run must:
- Start at $q_0$ 
- Loop at $q_0$ for $k$ steps (where $0 \le k \le n-1$)
- Transition to $q_1$ 
- Loop at $q_1$ for $n-k-1$ steps

For a run that transitions to $q_1$ at position $k+1$:

$$\text{weight} = \lambda(q_0) \cdot \mu(q_0,a,q_0)^k \cdot \mu(q_0,a,q_1) \cdot \mu(q_1,a,q_1)^{n-k-1} \cdot \gamma(q_1)$$
$$= 1 \cdot 1^k \cdot 1 \cdot 1^{n-k-1} \cdot 1 = 1$$

Since there are $n$ possible positions to make the transition (at steps $1, 2, \ldots, n$), we have $n$ distinct runs, each with weight $1$.

Therefore:
$$[\![A]\!](a^n) = \sum_{k=0}^{n-1} 1 = n$$

Unable to figure the proof for the latter part. will ask the TF to help. 