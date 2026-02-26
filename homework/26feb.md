### Simulation of a $k$-tape TM by a 1-tape TM

Claim: Let $M$ be a deterministic $k$-tape Turing machine that on every input of length $n$ halts within time $T(n)$. Then there exists a deterministic single-tape Turing machine $M'$ that decides the same language and runs in time $O(T(n)^2)$.

---

### Idea of the Simulation

- In $T(n)$ steps, each tape head of $M$ can move at most $T(n)$ cells away from its starting position.
- So, on any input of length $n$, each tape of $M$ uses at most $O(T(n))$ cells, and therefore all $k$ tapes together use at most $O(T(n))$ cells (up to a constant factor).
- We encode all $k$ tapes and their head positions on a single tape of $M'$.
- One step of $M$ will be simulated by $M'$ using a full scan of this encoding, which costs $O(T(n))$ time.
- Since $M$ does at most $T(n)$ steps, the total time of $M'$ will be $O(T(n)^2)$.

---

### Encoding of a Configuration on One Tape

A configuration of $M$ consists of:

- the current state $q$,
- the contents of each of the $k$ tapes,
- and the position of each tape head.

We encode this on the tape of $M'$ as follows:

- The tape of $M'$ is divided into $k$ blocks, one for each tape of $M$, separated by a special symbol $\#$.
- Inside each block we store the contents of that tape.
- To record the head position in a block, we use a marked version of the tape symbols: for every symbol $a$ of $M$ we add a dotted version ${a}$ to the alphabet of $M'$. In each block there is exactly one dotted symbol, and that cell is where the head of that tape currently is.

So the tape of $M'$ looks conceptually like

$
\#\; \ldots a \,{b}\, c \ldots \; \#\; \ldots {d} e \ldots \; \# \ldots
$

The control state $q$ of $M$ is stored in the finite control of $M'$. Thus each configuration of $M$ corresponds to exactly one configuration of $M'$.

---

### Simulating One Step

Suppose the transition function of $M$ is

$
\delta(q, a_1, a_2, \ldots, a_k)
  = (q', b_1, b_2, \ldots, b_k, d_1, d_2, \ldots, d_k),
$

where $a_i$ is the symbol currently under head $i$, $b_i$ is the symbol to be written, and $d_i \in \{L, R, S\}$ is the head movement on tape $i$.

To simulate one step of $M$, the single-tape machine $M'$ does the following:

1. Left-to-right scan:  
   $M'$ scans the entire used portion of its tape from left to right. In each block it finds the unique dotted symbol ${a_i}$. From these, it reads the tuple $(a_1, \ldots, a_k)$ while remembering the current state $q$ in its control.

2. Compute the transition:  
   Knowing $(q, a_1, \ldots, a_k)$, $M'$ uses its transition function (hard-wired in its finite control) to determine
   $
   (q', b_1, \ldots, b_k, d_1, \ldots, d_k).
   $

3. Right-to-left scan (or another full scan):  
   $M'$ now makes another scan over its tape. When it encounters ${a_i}$ in block $i$:
   - it replaces ${a_i}$ by the unmarked write symbol $b_i$,
   - moves left or right within the same block according to $d_i$,
   - and marks the new head position by turning that cell’s symbol into its dotted version.  
   If the head moves onto a previously blank cell, $M'$ extends the block by inserting a blank symbol (and marking it if needed).

4. Update state:  
   Finally, $M'$ changes its control state to $q'$.

Thus, one step of $M$ is simulated by a constant number of full scans of the used portion of the tape of $M'$.

---

### Time Analysis

During a computation of length $T(n)$:

- Each of the $k$ heads of $M$ can move at most $T(n)$ cells from its starting position.
- Hence, each tape of $M$ uses at most $T(n)$ cells, so all $k$ tapes together use at most $k \cdot T(n) = O(T(n))$ cells.

Our encoding for $M'$ adds:

- a constant number of separator symbols $\#$,
- and only a constant factor more symbols for dotted versions.

Therefore, at any point in the simulation, the used portion of the single tape of $M'$ has length

$
O(T(n)).
$

For each simulated step of $M$, $M'$ performs a constant number of full scans of this portion, so simulating one step of $M$ takes time

$
O(T(n)).
$

Since $M$ runs for at most $T(n)$ steps, the total running time of $M'$ on an input of length $n$ is

$
T(n) \cdot O(T(n)) = O(T(n)^2).
$

---

### Conclusion

We have described a deterministic single-tape Turing machine $M'$ that simulates the given deterministic $k$-tape Turing machine $M$. The simulation preserves acceptance and rejection of all inputs, and the running time satisfies

$
T_{M'}(n) = O(T(n)^2).
$

Thus, any deterministic $k$-tape TM running in time $T(n)$ can be simulated by a deterministic single-tape TM in time $O(T(n)^2)$
