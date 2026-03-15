# Context-free languages are not closed under quotient

The quotient of two languages $L_1$ and $L_2$ is
$
L_1 / L_2 = \{ x \mid \exists y \in L_2 \text{ such that } xy \in L_1 \}.
$

We give a CFL $L_1$ and a CFL $L_2$ such that $L_1 / L_2$ is not context-free.

Let
$
L_1 = \{ a^n b^n c^m \mid n, m \geq 0 \} \cup \{ a^n b^m c^m \mid n, m \geq 0 \}, \qquad
L_2 = \{ b^m c^m \mid m \geq 0 \}.
$

$L_1$ is context-free (union of two CFLs; each has a simple grammar). $L_2$ is context-free (e.g. $S \to bSc \mid \varepsilon$).

Computing $L_1 / L_2$: $x \in L_1 / L_2$ iff there exists $y \in L_2$ with $xy \in L_1$. Every $y \in L_2$ is of the form $b^j c^j$ for some $j \geq 0$.

- If $x = a^n$, then $xy = a^n b^j c^j$. This is in $L_1$ from the second part (take $m = j$). So $a^* \subseteq L_1 / L_2$.
- If $x = a^n b^k$ with $0 \leq k \leq n$, take $y = b^{n-k} c^{n-k}$ (so $j = n - k \geq 0$). Then $xy = a^n b^n c^{n-k}$, which is in the first part of $L_1$. So $\{ a^n b^k \mid 0 \leq k \leq n \} \subseteq L_1 / L_2$.
- No other form of $x$ can have $xy \in L_1$ for some $y = b^j c^j$, so
$
L_1 / L_2 = a^* \cup \{ a^n b^k \mid 0 \leq k \leq n \}.
$

We show $L_1 / L_2$ is not context-free. CFLs are closed under intersection with regular languages. So if $L_1 / L_2$ were a CFL, then $L' = (L_1 / L_2) \cap a^* b^* = a^* \cup \{ a^n b^k \mid 0 \leq k \leq n \}$ would be a CFL. Use the pumping lemma for CFLs on $L'$. Let $p$ be the pumping length and take $z = a^p b^p \in L'$. Then $z = uvwxy$ with $|vwx| \leq p$, $|vx| \geq 1$, and $uv^i wx^i y \in L'$ for all $i \geq 0$. So $vwx$ lies in some $a$'s, or in some $b$'s, or across the boundary. If $vx$ is contained in the $a$'s, then $uv^0 wx^0 y$ has fewer $a$'s than $b$'s, so it is not in $a^*$ and not in $\{ a^n b^k \mid k \leq n \}$. If $vx$ is contained in the $b$'s, pumping down gives more $a$'s than $b$'s, again not in $L'$. If $vx$ crosses the $a$–$b$ boundary, then pumping up gives a string with $a$'s and $b$'s interleaved or the counts violate $k \leq n$. So $L'$ does not satisfy the pumping lemma, so $L'$ is not context-free, hence $L_1 / L_2$ is not context-free.

So context-free languages are not closed under quotient.
