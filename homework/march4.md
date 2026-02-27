Q : Define the Output Turing Machine with the following modifications: it takes an input w if the word is accepted, the word w' denoting its tape contents at the moment of acceptance is its output. Construct an output Turing machine that takes in a number in unary and outputs the number in binary.


## what is an output turing machine

a normal TM just accepts or rejects. an output TM does the same thing but when it accepts, whatever is left on the tape is the output $w'$. so the tape at halt = the answer.

## the problem

input: a unary number, so $n$ is represented as $n$ ones. for example:

$$n = 5 \implies w = 11111$$

output: $n$ in binary. so for $n = 5$ we want $w' = 101$

---

## the idea

doing unary to binary directly in one shot is a bit annoying on a TM. the cleanest approach is:

1. repeatedly divide the unary count by 2, recording the remainder each time as a binary digit
2. then reverse the binary digits at the end

but a TM with a single tape makes this messy. so lets think of it more simply:

we use the tape to separate regions. the tape will look like:

$$\underbrace{1 \cdots 1}_{\text{remaining unary}} \# \underbrace{b_k \cdots b_0}_{\text{binary digits (LSB first)}}$$

the $\#$ acts as a separator.

---

## algorithm

repeat until unary part is empty:
- count the unary strokes. if even, append $0$ to binary section. if odd, append $1$.
- divide the unary count by 2 (remove every other stroke)

then reverse the binary section (since we built it LSB first).

---

## states and what they do

$q_0$ — scan the unary input, place a $\#$ at the end to separate regions

$q_{even}, q_{odd}$ — do a parity check pass over the unary block. we toggle between these two states as we scan each $1$, so after scanning the whole block the state tells us whether $n$ was even or odd

$q_{write0}, q_{write1}$ — go to the end of the tape (past $\#$) and write $0$ or $1$ accordingly (the next LSB)

$q_{halve}$ — go back and remove every other $1$ from the unary block (this divides by 2, rounding down)

$q_{reverse}$ — once unary block is empty, reverse the binary string on the right of $\#$

$q_{accept}$ — clean up the $\#$ and accept, leaving just the binary string on tape

---

## transition sketch

### phase 1 — parity check

scan left to right over the unary block toggling state:

$$\delta(q_{even}, 1) = (q_{odd}, 1, R)$$
$$\delta(q_{odd}, 1) = (q_{even}, 1, R)$$

when we hit $\#$:

$$\delta(q_{even}, \#) = (q_{write0}, \#, R)$$
$$\delta(q_{odd}, \#) = (q_{write1}, \#, R)$$

### phase 2 — write binary digit

move right past any existing binary digits to the first blank, write the new digit:

$$\delta(q_{write0}, 0) = (q_{write0}, 0, R)$$
$$\delta(q_{write0}, 1) = (q_{write0}, 1, R)$$
$$\delta(q_{write0}, \sqcup) = (q_{halve}, 0, L) \quad \text{then rewind left}$$

same for $q_{write1}$ but writes $1$.

### phase 3 — halve the unary block

rewind to start of tape, then scan and delete every other $1$.  after this pass the unary count is $\lfloor n/2 \rfloor$.

if the unary block is now empty (only $\#$ and binary digits remain), go to $q_{reverse}$.

### phase 4 — reverse binary string

standard TM reversal: repeatedly take the first binary digit, move it to the end, shrink. this flips LSB-first into MSB-first.

then accept — tape holds the binary representation.

---

## example trace for $n = 3$, input $111$

initial tape: $111$

after placing separator: $111\#$

round 1: scan $111$ → 3 ones → odd → write $1$ → halve → $1\#1$ (unary part is now $\lfloor 3/2 \rfloor = 1$)

round 2: scan $1$ → 1 one → odd → write $1$ → halve → $\#11$ (unary empty)

round 3: unary empty, binary section is $11$ (LSB first = $11$ in this case, which reversed is still $11$)

output: $11$ which is $3$ in binary. 

