- $\Sigma_1^P = \{L\ |\ \exists \text{ a polynomial-time predicate } R$ s.t. $x \in L \iff \exists y_1: R(x, y_1)$, where $|y_1|$ is bounded by a polynomial in $|x| \}$
- $\Pi_1^P = \{L\ |\ \exists \text{ poly-time } R$ s.t. $x \in L \iff \forall y_1: R(x, y_1)\}$

This is exactly the definition of $NP$:  
A language $L$ is in $NP$ if there is a polynomial-time predicate/verifier $R(x, y_1)$ such that $x \in L$ iff there exists $y_1$ of polynomially bounded length so that $R(x, y_1)$ accepts.  
Hence, $\Sigma_1^P = NP$.

Similarly, $\Pi_1^P$ consists of all languages whose membership can be verified by a poly-time predicate $R$ for which $x \in L \iff \forall y_1,\ R(x, y_1)$ holds.  
This is exactly the definition of the complement of $NP$, i.e., $\Pi_1^P = coNP$.


To show $\Sigma_k^P \subseteq \Sigma_{k+1}^P$ and $\Pi_k^P \subseteq \Pi_{k+1}^P$ for all $k$:

Let $L \in \Sigma_k^P$.  
By definition, there exists a polynomial-time predicate $R$ such that:
$$
x \in L \iff \exists y_1 \forall y_2 \exists y_3 \cdots Q_k y_k: R(x, y_1, \ldots, y_k)
$$

But $\Sigma_{k+1}^P$ is defined as languages of the form:
$$
x \in L' \iff \exists z_1 \forall z_2 \exists z_3 \cdots Q_{k+1} z_{k+1}: S(x, z_1, \ldots, z_{k+1})
$$

To express $L$ in $\Sigma_{k+1}^P$, just add a useless (dummy) quantifier at the end:
$$
x \in L \iff \exists y_1 \forall y_2 \cdots Q_k y_k \exists y_{k+1}: R(x, y_1, \ldots, y_k)
$$

where $y_{k+1}$ is ignored by $R$. This shows every predicate/structure in $\Sigma_k^P$ can be written in $\Sigma_{k+1}^P$, so  
$\Sigma_k^P \subseteq \Sigma_{k+1}^P$.

Similarly, $\Pi_k^P \subseteq \Pi_{k+1}^P$ (by adding an extra unused quantifier at the end).

Now, consider $\Sigma_k^P = co\, \Pi_k^P$ (complement):

Let $L \in \Sigma_k^P$.  
By definition, there exists $R$ such that:
$x \in L \iff \exists y_1 \forall y_2 \exists y_3 \cdots Q_k y_k: R(x, y_1, \ldots, y_k)$

The complement set $L^c$ is all $x$ for which the above is false.  
Negating the quantifiers alternates their type:
$x \notin L \iff \neg [\exists y_1 \forall y_2 \exists y_3 \cdots Q_k y_k: R(x, y_1, \ldots, y_k)]$,  
which is equivalent to  
$\forall y_1 \exists y_2 \forall y_3 \cdots Q_k' y_k: \neg R(x, y_1, \ldots, y_k)$
This quantifier string is exactly the definition of $\Pi_k^P$ (with predicate $\neg R$).  
Therefore, the complement of any $\Sigma_k^P$ language is in $\Pi_k^P$:
$co\,\Sigma_k^P = \Pi_k^P$, and thus $\Sigma_k^P = co\, \Pi_k^P$.
