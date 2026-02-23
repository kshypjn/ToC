Let $M$ be a 1-counter machine. I view its counter as a nonnegative integer $k$.

To get a pushdown automaton $P$, I let the stack store $k$ in unary: the stack has a bottom marker $Z_0$ and then $k$ copies of a symbol $X$. So “counter $= k$” corresponds to stack contents $Z_0 X^k$. An increment of the counter is simulated by pushing one $X$; a decrement (only when $k>0$) is simulated by popping one $X$; and a zero-test is just checking that the top of stack is $Z_0$. The control states and input behaviour are copied from $M$. Hence every step of $M$ is simulated by a constant number of moves of $P$, so any 1-counter language is context-free.

For the converse, I give a CFL that no 1-counter machine can recognize. Take
$$
L = \{ w c w^R \mid w \in \{a,b\}^* \},
$$
where $c$ is a separator. A PDA for $L$ first reads $w$ and pushes its symbols onto the stack, then after reading $c$ it pops and matches them against the rest of the input; this is standard.

Intuitively a 1-counter machine is much weaker: at any time it only remembers one integer (the counter value) plus a finite state. While reading the left half $w$ it can at best remember some function of $|w|$, but not the whole pattern of $a$’s and $b$’s. For long enough $w$ there will be two different words $w_1 \neq w_2$ for which the machine reaches exactly the same configuration after reading $w_1$ and $w_2$. From that point on it must behave identically on $w_1 c w_1^R$ and $w_2 c w_1^R$, so it would accept a non-member of $L$, a contradiction.

Therefore a PDA can simulate any 1-counter machine, but not vice versa.

