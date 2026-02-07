
A weighted automaton is $\mathcal{A} = (Q, \Sigma, \delta, \lambda, \rho)$
The weight of a string $w = a_1 a_2 \cdots a_n$ is computed as:

$$\mathcal{A}(w) = \sum_{\text{paths } q_0 \to q_n} \lambda(q_0) \cdot \delta(q_0, a_1, q_1) \cdot \delta(q_1, a_2, q_2) \cdots \delta(q_{n-1}, a_n, q_n) \cdot \rho(q_n)$$

For the empty string $\varepsilon$:

$$\mathcal{A}(\varepsilon) = \sum_{q \in Q} \lambda(q) \cdot \rho(q)$$

### Automaton for Geometric Distribution

construct $\mathcal{A} = (Q, \{a\}, \delta, \lambda, \rho)$ as follows:

States: $Q = \{q_0\}$ (single state)

Initial weight: $\lambda(q_0) = 1$

Final weight: $\rho(q_0) = 1 - \alpha$

Transition weight: $\delta(q_0, a, q_0) = \alpha$

For the string $a^k$ :

$$\mathcal{A}(a^k) = \lambda(q_0) \cdot \underbrace{\delta(q_0, a, q_0) \cdot \delta(q_0, a, q_0) \cdots \delta(q_0, a, q_0)}_{k \text{ transitions}} \cdot \rho(q_0)$$

$$= 1 \cdot \alpha^k \cdot (1 - \alpha) = (1 - \alpha) \alpha^k$$

**Diagram:**

```
        α
    ┌─────┐
    │     │
    ▼     │
→ (q₀) ───┘
    │
    │ (1-α)
    ▼
   ⊙ (accept)
```


where the initial arrow indicates $\lambda(q_0) = 1$ and the final weight is $(1-\alpha)$.

The distribution $D(\alpha, m, c)$ assigns weight $(1 - \alpha) \alpha^k$ to strings of the form $a^{mk + c}$ and assigns weight $0$ to all other strings.

Now I'll show that this can be represented by a weighted automaton.
States: $Q = \{q_0, q_1, q_2, \ldots, q_{m-1}\}$

Initial weight: $\lambda(q_0) = 1$, $\lambda(q_i) = 0$ for $i \neq 0$

Final weight: $\rho(q_c) = 1 - \alpha$, $\rho(q_i) = 0$ for $i \neq c$

Transition weights:
- For $i \neq c$: $\delta(q_i, a, q_{(i+1) \bmod m}) = 1$
- For $i = c$: $\delta(q_c, a, q_{(c+1) \bmod m}) = \alpha$

Verifying the construction : 
For a string $a^\ell$:

Case 1: If $\ell \not\equiv c \pmod{m}$, then the path ends in state $q_{\ell \bmod m} \neq q_c$, so $\rho(q_{\ell \bmod m}) = 0$, giving weight $0$. 

Case 2: If $\ell = mk + c$ for some $k \geq 0$:

The path is:
$$q_0 \xrightarrow{a} q_1 \xrightarrow{a} \cdots \xrightarrow{a} q_c \xrightarrow{a} q_{c+1} \xrightarrow{a} \cdots \xrightarrow{a} q_c \xrightarrow{a} \cdots \xrightarrow{a} q_c$$

- First $c$ transitions: $q_0 \to q_1 \to \cdots \to q_c$ with weights for all as 1
- Then $k$ complete cycles from $q_c$ back to $q_c$, each cycle has:
  - Transition $q_c \xrightarrow{a} q_{c+1}$ with weight $\alpha$
  - Next $m-1$ transitions with weight $1$ each, returning to $q_c$

Each complete cycle contributes weight $\alpha \cdot 1^{m-1} = \alpha$.

Total weight:
$$\mathcal{A}(a^{mk+c}) = \lambda(q_0) \cdot 1^c \cdot \alpha^k \cdot \rho(q_c) = 1 \cdot 1 \cdot \alpha^k \cdot (1-\alpha) = (1-\alpha)\alpha^k$$


### Diagram for D(α, m, c)

For example, with $m = 3$ and $c = 1$:

```
      1         1         α
  → q₀ ──→ q₁ ──→ q₂ ──→ q₀
            │       ↑     │
            │   1   │     │
            └───────┘     │ 1
                          ▼
                         q₀
```


```
            1              1
        q₀ ───→ q₁ ───────→ q₂
        ↑                    │
        │         α          │
        └────────────────────┘
             
        ρ(q₁) = 1-α
```

