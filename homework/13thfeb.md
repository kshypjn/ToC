(i) $L_1 = \{w \in \Sigma^* \mid w \text{ contains at least one } a\}$

$$\boxed{\Sigma^* \cdot a \cdot \Sigma^*}$$

This expression matches any string with at least one $a$ anywhere: (any string) followed by $a$ followed by (any string).
**Examples:**

- $a \in L_1$
- $ba \in L_1$
- $abab \in L_1$

(ii) $L_2 = (ab)^* = \{\epsilon, ab, abab, ababab, \ldots\}$
:

$$\boxed{\overline{\Sigma^* \cdot aa \cdot \Sigma^* \cup \Sigma^* \cdot bb \cdot \Sigma^* \cup \Sigma^* \cdot ba \cdot \Sigma^* \cup \Sigma \cdot (\Sigma\Sigma)^*}}$$

A string is in $(ab)^*$ if and only if it does not contain:

- The substring $aa$, OR
- The substring $bb$, OR
- The substring $ba$, OR
- Odd length

The first three conditions ensure alternation between $a$ and $b$. The fourth ensures the pattern starts with $a$ (if non-empty) and has even length.

