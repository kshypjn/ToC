Given a language $L$ that is recursively enumerable (RE) but not recursive. Let $L' = \{0w \mid w \in L\} \cup \{1w \mid w \notin L\}$, i.e., $L'$ contains all strings starting with $0$ whose suffix is in $L$ and all strings starting with $1$ whose suffix is not in $L$. Clearly, $0w \in L' \iff w \in L$ and $1w \in L' \iff w \notin L$.

We use many-one reductions: recall that if $A \le_m B$ and $B$ is recursive, then $A$ is recursive; if $A \le_m B$ and $B$ is RE, then $A$ is RE.

1. $L'$ is not recursive: Consider $f(w) = 0w$, which is computable and satisfies $w \in L \iff 0w \in L'$, so $L \le_m L'$. If $L'$ were recursive, $L$ would be recursive (contradiction), so $L'$ is not recursive.

2. $L'$ is not RE: Consider $g(w) = 1w$, which gives $w \notin L \iff 1w \in L'$, so $\overline{L} \le_m L'$. If $L'$ were RE, then $\overline{L}$ would be RE, but since $L$ is RE and not recursive, $\overline{L}$ is not RE. Contradiction; thus, $L'$ is not RE, and therefore also not recursive.

3. The complement: $\overline{L'} = \{0w \mid w \notin L\} \cup \{1w \mid w \in L\}$. Clearly, $1w \in \overline{L'} \iff w \in L$ and $0w \in \overline{L'} \iff w \notin L$, so $L \le_m \overline{L'}$ via $w \mapsto 1w$ and $\overline{L} \le_m \overline{L'}$ via $w \mapsto 0w$. If $\overline{L'}$ were recursive, $L$ would be recursive (contradiction). If $\overline{L'}$ were RE, then $\overline{L}$ would be RE (contradiction again), so $\overline{L'}$ is not recursive and not RE.
