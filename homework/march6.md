Q : Construct a Turing machine that takes as input a number n in unary and accepts if and only if n is a perfect square.

---

## the idea

a perfect square is a number like $0, 1, 4, 9, 16, 25, \ldots$ basically $n = k^2$ for some $k \geq 0$.

there's a neat trick here. notice that:

$$k^2 = 1 + 3 + 5 + \cdots + (2k-1)$$

so $n$ is a perfect square if and only if you can subtract successive odd numbers $1, 3, 5, 7, \ldots$ from $n$ until you hit exactly $0$. if you overshoot (go negative), reject.

for example $n = 9$: $9 - 1 = 8$, $8 - 3 = 5$, $5 - 5 = 0$. accept.

for example $n = 7$: $7 - 1 = 6$, $6 - 3 = 3$, $3 - 5 = -2$. overshot. reject.

this is perfect for a TM because we can do subtraction by crossing off $1$s.

---

## tape setup

input is $n$ ones:

$$\underbrace{1\ 1\ 1\ \cdots\ 1}_{n}$$

we'll cross off ones using $X$. the TM repeatedly removes the next odd number of ones from the remaining block.

---

## states

$q_0$ — start of each round, try to remove one more $1$ (the "first" stroke of the current odd number)

$q_{skip}$ — we've removed the first stroke of the current odd chunk, now skip over already-removed strokes to continue removing

$q_{check}$ — tape might be all $X$'s, check if we're done (accept) or still have ones left

$q_{back}$ — rewind to the left to start the next round

$q_{accept}$ — perfect square, accept

$q_{reject}$ — not a perfect square, reject

we also need a way to track how many ones to remove in the current round. the $i$-th round removes $2i - 1$ ones. we handle this by keeping a small "counter" region on the tape, but the simplest TM approach is just to interleave the removal carefully:

in round $i$, we need to remove $2i-1$ ones. we can do this by maintaining a secondary set of marks. but let me describe a cleaner version:

---

we use two symbols:

- $X$ — a one that's been permanently crossed off (part of a completed odd subtraction)
- $Y$ — a temporary mark used during the current round

the idea each round:

1. mark one $1$ as $Y$ (this accounts for the first $1$ of the odd number $2i-1$)
2. then for each existing $X$ group on the tape, mark two more $1$s as $Y$
3. convert all $Y$s to $X$s
4. if at any point there aren't enough $1$s left, reject
5. if after conversion the tape has no $1$s left, accept

the reason step 2 works: after round $i-1$, we need to remove $2i-1 = 2(i-1)+1$ ones in round $i$. that's one $1$ plus two for each previous round completed. so we mark $1$ initially then expand by $2$ for each prior round.

---

## transition sketch

### $q_0$ — beginning of each round

scan right, find first $1$, mark it $Y$, go to $q_{expand}$

if we see only $X$s and then $\sqcup$ with no $1$s left, go to $q_{accept}$

if tape is empty from the start (n=0), accept immediately:

$$\delta(q_0, \sqcup) = (q_{accept}, \sqcup, R)$$

### $q_{expand}$ — for each existing $X$, mark two more $1$s

scan right. each time we pass an $X$ we owe two more marked $1$s. find the next unmarked $1$s and mark them $Y$. if we run out of $1$s before we're done, go to $q_{reject}$.

### $q_{convert}$ — turn all $Y$s into $X$s

scan tape, replace every $Y$ with $X$.

### rewind — back to $q_0$

rewind to the leftmost cell, go back to $q_0$ for the next round.

---

## example: $n = 4$, input $1111$

round 1 (remove $2(1)-1 = 1$ one):

- mark one $1 \to Y$: tape is $Y111$
- no prior $X$s so no expansion needed
- convert $Y \to X$: tape is $X111$

round 2 (remove $2(2)-1 = 3$ ones):

- mark one $1 \to Y$: tape is $XY11$
- one prior $X$ so mark two more $1$s: tape is $XYYY$
- convert: tape is $XXXX$

back to $q_0$, scan right, only $X$s, hit $\sqcup \to$ accept.

$4 = 2^2$ ✓


