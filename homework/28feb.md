

1. $L$ is accepted by a 2-counter machine.
2. $L$ is not accepted by any 1-counter machine (and hence not by any pushdown automaton).



1. A 2-counter machine for $L$

A 2-counter machine consists of a finite control plus two nonnegative integer registers $C_1, C_2$. The operations allowed are increment, decrement (when nonzero), and test for zero.

The algorithm for processing an input word over $\{a, b, c\}$ is as follows:

1. Initialisation: Set $C_1 = 0$, $C_2 = 0$.

2. Phase 1 (scan the $a$'s):  
   While the input symbol is $a$, move right and increment $C_1$.  
   If the first symbol is $b$ or $c$, reject.  
   When the first non $a$ symbol is found, switch in the finite control to the $b$-phase.  
   If no $a$ is seen, reject (since $n \ge 1$).

3. Phase 2 (scan the $b$'s):  
   While the input symbol is $b$, do the following:  
   decrement $C_1$ (if $C_1 = 0$ then reject),  
   increment $C_2$,  
   move right.  
   When the first non-$b$ symbol is seen:  
   if it is not $c$, reject.  
   If no $b$ is seen, reject.  
   Switch to the $c$-phase.

4. Phase 3 (scan the $c$'s):  
   While the input symbol is $c$, do the following:  
   decrement $C_2$ (if $C_2 = 0$ then reject),  
   move right.  
   When the end of input is reached:  
   accept if and only if $C_2 = 0$ and the tape is exactly at the right endmarker.  
   Since in phase 2 we made sure not to decrement $C_1$ below 0, ending with $C_2 = 0$ means $C_1$ must also be 0 and all three blocks have the same length.

This machine checks that the input has form $a^* b^* c^*$, and the way the counters are updated ensures that the numbers of $a$'s, $b$'s, and $c$'s are all equal. Thus a 2-counter machine can accept $L$.

2. Why no 1-counter machine (and no PDA) can accept $L$

A 1-counter machine is strictly weaker: it has just one nonnegative integer counter $C$ and a finite control. In fact, a 1-counter machine is equivalent to a pushdown automaton with a stack alphabet of size 2 (one symbol for "counter $>$ 0" plus a bottom marker). Therefore any language accepted by a 1-counter machine is context-free.

But
$L = \{a^n b^n c^n \mid n \ge 1\}$
is not context-free.

Here is a sketch of the usual pumping lemma proof for context-free languages:

Assume, for contradiction, that $L$ is context-free. By the pumping lemma for context-free languages, there exists a pumping length $p$ such that any word $z \in L$ with $|z| \ge p$ can be decomposed as
$z = uvwxy$
with the properties:

1. $|vwx| \le p$
2. $|vx| \ge 1$
3. For all $i \ge 0$, the word $uv^i w x^i y \in L$

Let us choose the word
$z = a^p b^p c^p \in L$.
The substring $vwx$ has length at most $p$, so it must lie entirely within a single block of $a$'s, $b$'s, or $c$'s, or span at most two neighboring blocks (for example, some $a$'s and $b$'s, or some $b$'s and $c$'s). In all cases, if we pump $v$ and $x$ (take $i = 0$ or $i = 2$), the number of symbols in at most two of the three blocks changes, but not in all three at the same time. This destroys the equality of the three counts, and $uv^i w x^i y \notin L$ for some $i$, a contradiction.

Therefore, $L$ is not context-free. So no pushdown automaton, and in particular, no 1-counter machine can accept $L$.

Hence, $L$ can be accepted by a 2-counter machine, but not by any 1-counter machine (or PDA).
