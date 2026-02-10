
## (i) Prove that {ε} + R·R* = R*

need to show $\lbrace\varepsilon\rbrace \cup R \cdot R^* = R^*$.

$R^* = \lbrace\varepsilon\rbrace \cup R \cup R^2 \cup R^3 \cup \cdots$

**Direction 1:** Show $\lbrace\varepsilon\rbrace \cup R \cdot R^* \subseteq R^*$

- Clearly $\lbrace\varepsilon\rbrace \subseteq R^*$ since $\varepsilon \in R^*$ by definition
- For $R \cdot R^*$: any string in $R \cdot R^*$ has the form $w = w_1 w_2$ where $w_1 \in R$ and $w_2 \in R^*$
- If $w_2 = \varepsilon$, then $w = w_1 \in R \subseteq R^*$
- If $w_2 \in R^k$ for some $k \geq 1$, then $w \in R^{k+1} \subseteq R^*$
- Therefore $R \cdot R^* \subseteq R^*$

**Direction 2:** Show $R^* \subseteq \lbrace\varepsilon\rbrace \cup R \cdot R^*$

- For $\varepsilon$: clearly $\varepsilon \in \lbrace\varepsilon\rbrace \subseteq \lbrace\varepsilon\rbrace \cup R \cdot R^*$
- For any $w \in R^k$ where $k \geq 1$: we can write $w = w_1 w_2 \cdots w_k$ where each $w_i \in R$
- Then $w = w_1 \cdot (w_2 w_3 \cdots w_k)$ where $w_1 \in R$ and $(w_2 w_3 \cdots w_k) \in R^{k-1} \subseteq R^*$
- So $w \in R \cdot R^*$

Therefore $\lbrace\varepsilon\rbrace \cup R \cdot R^* = R^*$.

## (ii) Prove that R·R* = R⁺

$R \cdot R^* = R^+$:

$R^+ = R \cup R^2 \cup R^3 \cup \cdots$ (strings requiring at least one element from R)

This follows immediately from:
- $R \cdot R^* = R \cdot (\lbrace\varepsilon\rbrace \cup R \cup R^2 \cup \cdots)$
- $= R \cup R^2 \cup R^3 \cup \cdots = R^+$

Therefore $R \cdot R^* = R^+$. 

## (iii) If X = (R·X) ∪ S, then X = R*·S

