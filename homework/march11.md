We are given the language $L=\{\langle M\rangle \mid L(M)=\emptyset\}$ over descriptions of Turing machines $M$.

1. $L$ is not in RE.

Recall that
$HALT=\{\langle M,w\rangle \mid M \text{ halts on input } w\}$
is RE-complete and not decidable, and that its complement
$\overline{HALT}=\{\langle M,w\rangle \mid M \text{ does not halt on input } w\}$
is not in RE (otherwise both $HALT$ and $\overline{HALT}$ would be in RE, so $HALT$ would be decidable).

We reduce $\overline{HALT}$ to $L$. Given an input $\langle M,w\rangle$, we effectively construct a Turing machine $N$ such that
$L(N)=\emptyset \iff M \text{ does not halt on } w.$

Definition of $N$ on input $x$:

1. Ignore $x$ and simulate $M$ on input $w$.
2. If the simulation ever halts (accepting or rejecting), then immediately accept $x$.

- If $M$ does not halt on $w$, then in the computation of $N$ on any input $x$, step 1 never finishes, so $N$ never reaches the accepting step. Hence $N$ never accepts any input, so $L(N)=\emptyset$.
- If $M$ does halt on $w$, then for every input $x$, the simulation in step 1 eventually finishes, and then $N$ accepts $x$. So $L(N)=\Sigma^*$ is nonempty.

Therefore
$\langle M,w\rangle \in \overline{HALT} \iff L(N)=\emptyset \iff \langle N\rangle \in L.$
Thus there is a many-one reduction $\overline{HALT} \le_m L$. If $L$ were in RE, then $\overline{HALT}$ would also be in RE, which is impossible. Hence $L$ is not in RE.

2. $L$ is in co-RE.

To show that $L$ is in co-RE, it suffices to show that its complement
$\overline{L}=\{\langle M\rangle \mid L(M)\neq\emptyset\}$
is in RE, i.e., there is a Turing machine that semi-decides $\overline{L}$.

Idea: on input $\langle M\rangle$, we want to eventually accept if $M$ accepts at least one string, and otherwise run forever. We can do this by dovetailing over all possible inputs to $M$.

Define a Turing machine $D$ that on input $\langle M\rangle$ does:

1. For $k=1,2,3,\dots$ do the following stage:
   (a) Enumerate all strings $x$ over the input alphabet of $M$ of length at most $k$.
   (b) For each such $x$, simulate $M$ on input $x$ for $k$ steps (continuing earlier simulations from previous stages).
   (c) If any of these simulations reaches an accepting state, then accept $\langle M\rangle$.

If there exists some string $x$ such that $M$ accepts $x$, then for large enough $k$ the simulation of $M$ on $x$ will have been carried out for at least the number of steps in the real accepting computation, so $D$ will eventually see $M$ accept $x$ and will accept $\langle M\rangle$. Thus $\langle M\rangle\in\overline{L}$ implies $D$ accepts.

If $L(M)=\emptyset$, then $M$ never accepts any input, so $D$ never sees an accepting computation and therefore never accepts $\langle M\rangle$; it runs forever. Thus $D$ semi-decides $\overline{L}$.

Therefore $\overline{L}$ is in RE, so $L$ is in co-RE.