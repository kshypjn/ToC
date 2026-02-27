so the idea here is we need to build a Turing machine that accepts strings like $abcd$, $aabbccdd$, $aaabbbcccddd$ and also the empty string (since $n \geq 0$). it rejects anything else.

the basic strategy is: repeatedly cross off one $a$, one $b$, one $c$, and one $d$ at the same time, until everything is crossed off. if at any point the counts don't match, we reject.

---

## the alphabet

- input symbols: $\{a, b, c, d\}$
- tape symbols: $\{a, b, c, d, \hat{a}, \hat{b}, \hat{c}, \hat{d}, \sqcup\}$

where $\hat{a}, \hat{b}, \hat{c}, \hat{d}$ are "marked" versions of each symbol (already processed), and $\sqcup$ is the blank.

---

## high-level idea

each "round" does the following:

1. scan right to find the first unmarked $a$, mark it as $\hat{a}$
2. keep scanning right to find the first unmarked $b$, mark it as $\hat{b}$
3. keep scanning right to find the first unmarked $c$, mark it as $\hat{c}$
4. keep scanning right to find the first unmarked $d$, mark it as $\hat{d}$
5. go back to the start and repeat

when we scan from the beginning and find no more $a$'s, we check that there are also no remaining $b$'s, $c$'s, or $d$'s. if everything is fully marked, we accept.

---

## states

- $q_0$: start / look for an unmarked $a$
- $q_1$: found $\hat{a}$, now scan right looking for $b$
- $q_2$: found $\hat{b}$, now scan right looking for $c$
- $q_3$: found $\hat{c}$, now scan right looking for $d$
- $q_4$: found $\hat{d}$, now rewind to the left (go back to start)
- $q_{accept}$: accept
- $q_{reject}$: reject

---

## transition function

the tape head starts at the leftmost cell.

### in $q_0$ (looking for next $a$):

| read | write | move | next state |
|------|-------|------|------------|
| $a$ | $\hat{a}$ | R | $q_1$ |
| $\hat{a}$ | $\hat{a}$ | R | $q_0$ |
| $\sqcup$ | $\sqcup$ | R | $q_{accept}$ |
| $b, c, d, \hat{b}, \hat{c}, \hat{d}$ | — | — | $q_{reject}$ |

if we see a $b$, $c$, or $d$ before an $a$ it means things are out of order, so reject. if we only see blank it means everything was crossed off evenly.

### in $q_1$ (looking for a $b$ after marking $a$):

| read | write | move | next state |
|------|-------|------|------------|
| $a, \hat{a}, \hat{b}$ | same | R | $q_1$ |
| $b$ | $\hat{b}$ | R | $q_2$ |
| anything else (no $b$ found) | — | — | $q_{reject}$ |

### in $q_2$ (looking for a $c$ after marking $b$):

| read | write | move | next state |
|------|-------|------|------------|
| $b, \hat{b}, \hat{c}$ | same | R | $q_2$ |
| $c$ | $\hat{c}$ | R | $q_3$ |
| anything else | — | — | $q_{reject}$ |

### in $q_3$ (looking for a $d$ after marking $c$):

| read | write | move | next state |
|------|-------|------|------------|
| $c, \hat{c}, \hat{d}$ | same | R | $q_3$ |
| $d$ | $\hat{d}$ | R | $q_4$ |
| anything else | — | — | $q_{reject}$ |

### in $q_4$ (rewind to the left):

| read | write | move | next state |
|------|-------|------|------------|
| $\hat{a}, \hat{b}, \hat{c}, \hat{d}, a, b, c, d$ | same | L | $q_4$ |
| $\sqcup$ | $\sqcup$ | R | $q_0$ |

we just move left until we hit the blank on the left end, then go right one step and we're back at the beginning.

---

## example run

let's trace $w = aabbccdd$ (so $n = 2$):

round 1:
- mark first $a \to \hat{a}$, first $b \to \hat{b}$, first $c \to \hat{c}$, first $d \to \hat{d}$
- tape: $\hat{a} a \hat{b} b \hat{c} c \hat{d} d$

round 2:
- mark next $a \to \hat{a}$, next $b \to \hat{b}$, next $c \to \hat{c}$, next $d \to \hat{d}$
- tape: $\hat{a}\hat{a}\hat{b}\hat{b}\hat{c}\hat{c}\hat{d}\hat{d}$

round 3:
- back in $q_0$, we scan right, see only $\hat{a}$'s and then $\sqcup$ — accept!

---

## why it works

each round consumes exactly one $a$, one $b$, one $c$, one $d$. so if the string has $n$ of each, after $n$ rounds everything is marked and we accept. if at any point we can't find the next expected symbol in order, we reject. the language $\{a^n b^n c^n d^n \mid n \geq 0\}$ is actually not context-free, so we can't do this with a pushdown automaton — we need the full power of a Turing machine because we're essentially counting across four separate groups simultaneously.

the time complexity is $O(n^2)$ since we do $n$ passes and each pass is $O(n)$ long.