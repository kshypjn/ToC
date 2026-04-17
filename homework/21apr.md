
1. Prove that $NP^{NP} = \Sigma_2^P$ using the alternating quantifier definition.

Recall the alternating quantifier (logical) characterization of $\Sigma_k^P$:  
A language $L$ is in $\Sigma_k^P$ iff there is a polynomial-time predicate $P(x, y_1, \ldots, y_k)$ such that:  
$x \in L \iff \exists y_1 \forall y_2 \exists y_3 \cdots Q_k y_k\; P(x, y_1, \ldots, y_k) = 1$  
for $Q_i = \exists$ if $i$ is odd, $Q_i = \forall$ if $i$ is even.

For $\Sigma_2^P$, this gives $x \in L \iff \exists y_1 \forall y_2 : P(x, y_1, y_2) = 1$ for some polynomial-time predicate $P$.

$NP^{NP}$ is the class of problems solvable by an NP machine with an NP oracle. That means, on input $x$, the machine can:  
- Guess a witness $y_1$ (nondeterminism) of polynomial length.  
- Make calls to an NP oracle during its computation.

Each such computation can be rewritten as:  
"There exists $y_1$ such that for all possible oracle answers (each NP oracle call can be written as: there exists $y_2$ such that $R(z, y_2)$), the overall computation accepts $x$." In other words:  
$x \in L \iff \exists y_1 \forall y_2\; P(x, y_1, y_2) = 1$,  
where $P$ is a polynomial-time predicate.

Hence, $NP^{NP} = \Sigma_2^P$.

---

2. Show that $P^{NP} = \Delta_2^P$.

By definition,  
$\Delta_{k+1}^P = P^{\Sigma_k^P}$  
So,  
$\Delta_2^P = P^{\Sigma_1^P} = P^{NP}$  
Thus, $P^{NP} = \Delta_2^P$.

---

3. Prove that $NP^{NP^{NP}} = \Sigma_3^P$.

First, note that $\Sigma_3^P = NP^{\Sigma_2^P}$ by the recursive definition.

From above, $\Sigma_2^P = NP^{NP}$.

Plugging in:  
$\Sigma_3^P = NP^{\Sigma_2^P} = NP^{NP^{NP}}$

Therefore,  
$NP^{NP^{NP}} = \Sigma_3^P$.

Alternatively, in alternating quantifiers:  
A language $L \in NP^{NP^{NP}}$ if there exists an NP machine with access to an $NP^{NP}$ oracle. But $NP^{NP} = \Sigma_2^P$, which gives another definition of $\Sigma_3^P$.





