
For $k \geq 1$, define:

$
\Sigma_k^P = \{ L \mid \exists~\text{poly-time } R,~x \in L \iff \exists y_1~\forall y_2~\exists y_3~\cdots~Q_k y_k.~R(x, y_1, \ldots, y_k)\}
$

where the quantifiers alternate, starting with $\exists$ ($y_i$ are poly-length).  
Similarly, $\Pi_k^P$ starts with $\forall$.

---

**1. Show $\Sigma_1^P = NP$ and $\Pi_1^P = coNP$.**

For $k=1$:

$
\Sigma_1^P = \{ L \mid \exists~\text{poly-time } R,~x \in L \iff \exists y_1.~R(x, y_1) \}
$

This is precisely the definition of $NP$: there exists a polynomial-time verifier $R$ and a polynomial-length certificate $y_1$ such that $x \in L$ iff there exists $y_1$ with $R(x, y_1) = 1$.  
So, $\Sigma_1^P = NP$.

Similarly, for $\Pi_1^P$:

$
\Pi_1^P = \{ L \mid \exists~\text{poly-time } R,~x \in L \iff \forall y_1.~R(x, y_1) \}
$

Taking complements, $L \in \Pi_1^P \iff \overline{L} \in \Sigma_1^P \iff \overline{L} \in NP$. Hence, $\Pi_1^P = coNP$.

---

**2. Prove $\Sigma_k^P \subseteq \Sigma_{k+1}^P$, $\Pi_k^P \subseteq \Pi_{k+1}^P$ for all $k$.**

Any language $L$ in $\Sigma_k^P$ can be written as:

$
x \in L \iff \exists y_1~\forall y_2~\cdots~Q_k y_k.~R(x, y_1, \ldots, y_k)
$

But this can be rewritten as:

$
x \in L \iff \exists y_1~\forall y_2~\cdots~Q_k y_k~\exists y_{k+1}.~R(x, y_1, \ldots, y_k)
$

where $y_{k+1}$ is just ignored by $R$.  
Thus, the quantifier block can always be extended one step without changing the class, so:

$
\Sigma_k^P \subseteq \Sigma_{k+1}^P
$

The same argument works for $\Pi_k^P$, by adding an extra universal quantifier at the end.

---

**3. Show $\Sigma_k^P = co \Pi_k^P$.**

Let $L \in \Sigma_k^P$. Then, there is poly-time $R$ such that:

$
x \in L \iff \exists y_1~\forall y_2~\cdots~Q_k y_k.~R(x, y_1, \dots, y_k)
$

Take complement:

$
x \notin L \iff \forall y_1~\exists y_2~\cdots~\bar{Q}_k y_k.~\neg R(x, y_1, \dots, y_k)
$

This is a $\Pi_k^P$ predicate (the quantifiers alternate, starting with universal).

Thus, the complement of any $\Sigma_k^P$ language is in $\Pi_k^P$.  
Therefore, as sets:

$
\Sigma_k^P = co\Pi_k^P
$

and vice versa.



