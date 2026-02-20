Consider a system of polynomial equations over finite languages. Show that if this system has a solution then this solution is unique, and every component language of the solution is context-free language.

---

## Solution

### Setup

A polynomial equation over finite languages is an equation of the form:

$$
X = L_1 \cup L_2 \cdot X \cup L_3 \cdot X \cdot X \cup \cdots
$$

where:
- $X$ is a language variable (unknown language )
- $L_1, L_2, L_3, \ldots$ are finite languages (constants)
- $\cup$ is union
- $\cdot$ is concatenation

A system of such equations means we have multiple variables $X_1, X_2, \ldots, X_n$ and equations like:

$$
\begin{align}
X_1 &= f_1(X_1, X_2, \ldots, X_n) \\
X_2 &= f_2(X_1, X_2, \ldots, X_n) \\
&\vdots \\
X_n &= f_n(X_1, X_2, \ldots, X_n)
\end{align}
$$

where each $f_i$ is a polynomial expression (finite union of concatenations) over the variables and finite constant languages.

---

Uniqueness of Solution

We'll show that if a solution exists, it's unique using a fixed-point argument.

Key idea: Think of the system as defining a function $F: (\mathcal{P}(\Sigma^*))^n \to (\mathcal{P}(\Sigma^*))^n$ that maps an $n$-tuple of languages to another $n$-tuple by evaluating the right-hand sides.

A solution is a fixed point of $F$, i.e., $(L_1, \ldots, L_n)$ such that $F(L_1, \ldots, L_n) = (L_1, \ldots, L_n)$.

Claim: The function $F$ is monotone with respect to the subset ordering: if $(L_1', \ldots, L_n') \subseteq (L_1, \ldots, L_n)$ (component-wise), then $F(L_1', \ldots, L_n') \subseteq F(L_1, \ldots, L_n)$.

This is true because:
- Union and concatenation are monotone operations
- If $A \subseteq A'$ and $B \subseteq B'$, then $A \cup B \subseteq A' \cup B'$ and $A \cdot B \subseteq A' \cdot B'$
- Since all constants are finite (and thus fixed), monotonicity follows

Uniqueness argument:

Suppose we have two solutions: $(L_1, \ldots, L_n)$ and $(L_1', \ldots, L_n')$.

Consider the intersection $(L_1 \cap L_1', \ldots, L_n \cap L_n')$. Since $F$ is monotone and both tuples are fixed points:

$$
F(L_1 \cap L_1', \ldots, L_n \cap L_n') \subseteq F(L_1, \ldots, L_n) = (L_1, \ldots, L_n)
$$

and similarly

$$
F(L_1 \cap L_1', \ldots, L_n \cap L_n') \subseteq (L_1', \ldots, L_n')
$$

So $F(L_1 \cap L_1', \ldots, L_n \cap L_n') \subseteq (L_1 \cap L_1', \ldots, L_n \cap L_n')$.

Now, if $(L_1 \cap L_1', \ldots, L_n \cap L_n')$ is strictly smaller than both solutions, we can iterate $F$ starting from it and get a sequence that converges to a fixed point. But since both $(L_1, \ldots, L_n)$ and $(L_1', \ldots, L_n')$ are already fixed points, and the intersection is contained in both, we must have:

$$
(L_1 \cap L_1', \ldots, L_n \cap L_n') = (L_1, \ldots, L_n) = (L_1', \ldots, L_n')
$$

Therefore the solution is unique.


Showing that each component $L_i$ of the solution is a context-free language by constructing a context-free grammar for it.

Key idea: Since the right-hand sides involve only:
- Finite languages (which are regular, hence context-free)
- Union and concatenation operations

Construction:

For each variable $X_i$, we create a non-terminal $S_i$ in our grammar.

For each equation $X_i = f_i(X_1, \ldots, X_n)$, we translate the polynomial expression $f_i$ into production rules:

1. Finite constant languages: If $L = \{w_1, w_2, \ldots, w_k\}$ appears in the expression, add productions:
   $$
   S_i \to w_1 \mid w_2 \mid \cdots \mid w_k
   $$
   (where we treat each $w_j$ as a terminal string)

2. Concatenation: If the expression contains $L \cdot X_j$ (where $L$ is finite), add productions:
   $$
   S_i \to w_1 S_j \mid w_2 S_j \mid \cdots \mid w_k S_j
   $$
   for each $w_\ell \in L$.

3. Union: If the expression is $A \cup B$, we include productions from both $A$ and $B$.
Example: If $X = \{a\} \cup \{b\} \cdot X \cup \{c\} \cdot X \cdot X$, then:
$$
\begin{align}
S &\to a \\
S &\to bS \\
S &\to cSS
\end{align}
$$

This grammar generates exactly the language $X$.

