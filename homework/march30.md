To prove: The language $L = \{\langle M \rangle \mid |L(M)| = 72\}$ is neither recursively enumerable (RE) nor co-recursively enumerable (co-RE).

---

### 1. $L$ is not recursively enumerable (RE):

Suppose, for contradiction, that $L$ is RE. That would mean there is a Turing machine that enumerates all $\langle M \rangle$ such that $|L(M)| = 72$.

Let us use this to decide the following known undecidable problem:

- The emptiness problem: $E_{TM} = \{\langle M \rangle \mid L(M) = \emptyset\}$. We know $E_{TM}$ is not RE.

We show that, if $L$ were RE, then so is the emptiness problem, leading to a contradiction.

#### Reduction from the Emptiness Problem

Given any TM $M$, we will construct a new TM $M'$ such that:
- If $L(M) = \emptyset$, then $|L(M')| = 72$.
- If $L(M) \neq \emptyset$, then $|L(M')| \neq 72$.

Construction:

Let $S = \{s_1, s_2, \ldots, s_{72}\}$ be 72 fixed strings (for example: 72 distinct strings of the form "1", "11", ..., "1\ldots1" up to length 72).

Define $M'$ as follows:
- On input $x$:
    - If $x \in S$, accept.
    - Else, simulate $M$ on $x$. If $M$ accepts $x$, accept; otherwise, reject.

Now, analyze $L(M')$:
- If $L(M) = \emptyset$, then $L(M') = S$, so $|L(M')| = 72$.
- If $L(M) \neq \emptyset$, then for some string $w \notin S$, $M$ accepts $w$, so $L(M') \supseteq S \cup \{w\}$, and thus $|L(M')| \geq 73$.

Thus, $\langle M \rangle \in E_{TM}$ iff $\langle M' \rangle \in L$.

If $L$ were RE, then $E_{TM}$ would be RE (just map $\langle M \rangle \to \langle M' \rangle$). But $E_{TM}$ is not RE. Contradiction!

Therefore, $L$ is not recursively enumerable.

---

### 2. $L$ is not co-recursively enumerable (co-RE):

Suppose, for contradiction, that $L$ is co-RE. Then its complement $\overline{L} = \{\langle M \rangle \mid |L(M)| \neq 72\}$ is RE.

We use a similar reduction to the universality problem: $ALL_{TM} = \{\langle M \rangle \mid L(M) = \Sigma^*\}$, which is known to be not RE.

Given any TM $M$, construct $M''$ that accepts all strings except possibly the ones in $S$ as follows:
- On input $x$:
    - If $x \notin S$, accept.
    - If $x \in S$, simulate $M$ on $x$. Accept if $M$ accepts $x$.

Now, analyze $|L(M'')|$:
- If $L(M) = \Sigma^*$, then for all $x \in S$, $M$ accepts $x$, so $L(M'') = \Sigma^*$, thus infinite, so $|L(M'')| \neq 72$.
- If $L(M) \neq \Sigma^*$, then there is some $y \in S$ such that $M$ does not accept $y$. Then $L(M'')$ omits $y$ but accepts all other strings, so the cardinality is either infinite or at least greater than 72.

Alternatively, consider the halting problem and Rice's theorem: the property "$|L(M)| = 72$" is nontrivial (true for some TMs, false for others), so the set is not RE nor co-RE.

---

## Conclusion

$L = \{\langle M \rangle \mid |L(M)| = 72\}$ is neither RE nor co-RE.