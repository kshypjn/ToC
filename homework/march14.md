We are given a language $L$ that is recursively enumerable (RE) but not recursive 
Let 
$
L' = \{0w \mid w \in L\} \cup \{1w \mid \neg(w \in L)\}.
$
So $L'$ contains:
- all strings starting with $0$ whose suffix is in $L$, and
- all strings starting with $1$ whose suffix is not in $L$.

First,
$
0w \in L' \iff w \in L,
$
$
1w \in L' \iff w \notin L.
$

We will use many-one reductions. Recall that if $A \le_m B$ and $B$ is recursive, then $A$ is recursive. Also, if $A \le_m B$ and $B$ is RE, then $A$ is RE.

1. Show that $L'$ is not recursive:

Consider the function $f(w) = 0w$. This is a computable function, and for all $w$ we have
$
w \in L \iff 0w \in L'.
$
So this is a many-one reduction $L \le_m L'$. If $L'$ were recursive, then $L$ would also be recursive, contradicting the assumption that $L$ is not recursive. Therefore, $L'$ is not recursive.

2. Show that $L'$ is not RE:

Now consider the function $g(w) = 1w$. For all $w$ we have
$
w \notin L \iff 1w \in L'.
$
This gives a many-one reduction $\overline{L} \le_m L'$, where $\overline{L}$ is the complement of $L$. If $L'$ were RE, then $\overline{L}$ would be RE as well. But we know $L$ is RE and not recursive, so its complement $\overline{L}$ is not RE. This is a contradiction. Therefore, $L'$ is not RE.

Since $L'$ is not RE, it is also not recursive (which we already showed).

3. Classify the complement $\overline{L'}$:

We can write the complement explicitly:
$
\overline{L'} = \{0w \mid w \notin L\} \cup \{1w \mid w \in L\}.
$
We can do the same style of reductions:
$
1w \in \overline{L'} \iff w \in L,
$
$
0w \in \overline{L'} \iff w \notin L.
$
So $L \le_m \overline{L'}$ via $w \mapsto 1w$, and $\overline{L} \le_m \overline{L'}$ via $w \mapsto 0w$.

If $\overline{L'}$ were recursive, then $L$ would be recursive (contradiction). So $\overline{L'}$ is not recursive.

If $\overline{L'}$ were RE, then $\overline{L}$ would be RE as well (by the reduction $\overline{L} \le_m \overline{L'}$), which again contradicts that $L$ is RE but not recursive. So $\overline{L'}$ is not RE.

