

## the encoding

so a graph with $n$ vertices is stored as a flat $n \times n$ adjacency matrix. the entry at position $k = n \cdot i + j + 1$ (1-indexed) tells us whether there's an edge $i \to j$. for example with $n = 3$:

$$\underbrace{a_{00}\ a_{01}\ a_{02}}_{row\ 0}\ \underbrace{a_{10}\ a_{11}\ a_{12}}_{row\ 1}\ \underbrace{a_{20}\ a_{21}\ a_{22}}_{row\ 2}$$

we want to check: is there a directed path from vertex $0$ to vertex $n-1$?

---

## the idea — BFS/reachability by marking

we do a reachability check using a marking scheme directly on the tape. the idea is basically BFS: start with vertex $0$ marked as reachable, then repeatedly scan the adjacency matrix and mark any vertex reachable from an already-marked vertex. repeat until no new vertices get marked or vertex $n-1$ gets marked.

the problem is that $n$ is not given explicitly — we have to figure it out from the length of the input, since the input has length $n^2$.

---

## step 0 — figure out $n$

the input has length $n^2$ for some $n$. we need to find $n$. we do this by trying $n = 1, 2, 3, \ldots$ and checking whether the input length equals $n^2$. we can check this by marking off $n^2$ symbols in the standard TM way (like the $a^n b^n$ trick but for squares). once we find the right $n$, we store it implicitly via tape marks.

in practice the TM would use a second track or a tape region to keep a counter, but conceptually: find $n$ such that input length $= n^2$, then proceed.

if no such $n$ exists (input length is not a perfect square), reject immediately.

---

## step 1 — set up a "reachable" region

after the input we write a separator $\#$ followed by $n$ bits representing which vertices are currently known to be reachable. call this the reachability vector $R$:

$$\underbrace{w_1 w_2 \cdots w_{n^2}}_{\text{adjacency matrix}} \# \underbrace{r_0\ r_1\ \cdots\ r_{n-1}}_{\text{reachability vector}}$$

initialize $R$ to $10\cdots0$ (only vertex $0$ is reachable at the start).

---

## step 2 — one round of propagation

scan through every edge $i \to j$ in the adjacency matrix. the entry for edge $i \to j$ is at position $n \cdot i + j + 1$ in the input.

for each entry:
- if $w_{n \cdot i + j + 1} = 1$ (edge exists) and $r_i = 1$ (vertex $i$ is reachable), then set $r_j = 1$

to do this on a TM: for each position $k$ in the input, decode which $i$ and $j$ it corresponds to (by counting), then check $r_i$ in the reachability vector, and if the edge is $1$, update $r_j$.

---

## step 3 — repeat until stable or done

after each full pass over the adjacency matrix:

- check if $r_{n-1} = 1$. if yes, accept.
- check if anything changed in $R$ during this pass. if nothing changed, we've reached a fixed point and vertex $n-1$ is not reachable — reject.
- otherwise do another pass.

since there are only $n$ vertices, after at most $n$ rounds either we've marked vertex $n-1$ or we never will.

---

## example: $n = 3$, input $010001100$

the adjacency matrix is:

$$\begin{pmatrix} 0 & 1 & 0 \\ 0 & 0 & 1 \\ 1 & 0 & 0 \end{pmatrix}$$

so edges are: $0 \to 1$, $1 \to 2$, $2 \to 0$.

we want a path from vertex $0$ to vertex $2$.

reachability vector starts as $R = 100$.

round 1:
- scan edge $0 \to 1$: input bit $= 1$, $r_0 = 1$ $\Rightarrow$ set $r_1 = 1$. now $R = 110$
- scan edge $1 \to 2$: input bit $= 1$, $r_1 = 1$ $\Rightarrow$ set $r_2 = 1$. now $R = 111$

check $r_2 = 1$ $\Rightarrow$ accept. there is a path $0 \to 1 \to 2$. 

