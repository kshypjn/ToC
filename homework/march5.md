Q: Construct a Turing machine that takes as input a number n in unary and accepts if and only if n is a perfect square.


## the idea

a perfect square is a number like $0, 1, 4, 9, 16, 25, \ldots$ basically $n = k^2$ for some $k \geq 0$.

there's a neat trick here. notice that:

$$k^2 = 1 + 3 + 5 + \cdots + (2k-1)$$

so $n$ is a perfect square if and only if you can subtract successive odd numbers $1, 3, 5, 7, \ldots$ from $n$ until you hit exactly $0$. if you overshoot (go negative), reject.

for example $n = 9$: $9 - 1 = 8$, $8 - 3 = 5$, $5 - 5 = 0$. accept.

for example $n = 7$: $7 - 1 = 6$, $6 - 3 = 3$, $3 - 5 = -2$.  reject.


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
2. then for each existing $Y$ on the tape (from previous rounds acting as our counter), mark two more $1$s as $Y$
3. convert all $Y$s to $X$s
4. if at any point there aren't enough $1$s left, reject
5. if after conversion the tape has no $1$s left, accept

wait — let me explain why step 2 works. after round $i-1$ there are $i-1$ groups of $Y \to X$ markings. in round $i$ we need to remove $2i-1$ ones. note $2i - 1 = 2(i-1) + 1$, so we remove one $1$ plus two for each previous round. that's exactly what step 2 does.

---

## transition sketch

### beginning of each round — $q_0$

scan right, find first $1$, mark it $Y$, go to $q_{expand}$

if we only see $X$s and $Y$s and then $\sqcup$ with no $1$s left, go to $q_{check}$

### $q_{expand}$ — for each existing $Y$, mark two more $1$s

scan right over the tape. each time we see a $Y$ we "owe" two more $1$s to be marked. find the next two unmarked $1$s and mark them $Y$. if we can't find enough $1$s, go to $q_{reject}$.

### $q_{convert}$ — turn all $Y$s into $X$s

scan tape, replace every $Y$ with $X$.

### back to $q_0$ — rewind and repeat

rewind to start, go back to $q_0$ for the next round.

### $q_{check}$

scan the whole tape. if only $X$s remain (no $1$s), go to $q_{accept}$. if any $1$s remain, go to $q_{reject}$.

---

## example: $n = 4$ (input $1111$)

round 1 (remove $1$ one):
- mark one $1$ as $Y$: $Y111$
- no existing $Y$s to expand from (other than the one we just placed, which is the seed)
- actually: we mark 1 one (that's $2(1)-1 = 1$)
- convert: $X111$

round 2 (remove $3$ ones):
- mark one $1$ as $Y$: $XY11$
- one existing $X$ group means we need $2$ more $\to$ mark two more $1$s: $XYYY$
- convert: $XXXX$

now scan: no $1$s left $\to$ accept. $4 = 2^2$, correct.

---

## example: $n = 6$ (input $111111$)

round 1 (remove $1$): tape becomes $X11111$

round 2 (remove $3$): tape becomes $XXXX11$

round 3 (remove $5$): need to mark $5$ ones, only $2$ left $\to$ not enough $\to$ reject.

$6$ is not a perfect square, correct.

