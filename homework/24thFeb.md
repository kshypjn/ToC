Let the deterministic Turing machine be $M = (Q, \Gamma, \Sigma, \delta, q_0, q_{\text{acc}}, q_{\text{rej}})$, where $\Gamma$ is the tape alphabet (containing the blank symbol $\sqcup$), and $\Sigma \subseteq \Gamma$ is the input alphabet.

Idea: at any time, the Turing machine has the tape divided at the head position:

- the portion strictly to the left of the head, written from left to right;
- the symbol currently under the head;
- the portion strictly to the right of the head, written from left to right.

We represent these using two stacks:

- Stack 1 holds the tape contents to the left of the head, with the cell immediately left of the head on the top, then the next one further left beneath it, etc.;
- Stack 2 holds the cell under the head and all cells to the right, with the symbol currently under the head on the top, then the next cell to the right beneath it, etc.

Thus the pair (stack 1, stack 2) encodes the entire tape and the head position.

### Initialisation

On input $w = a_1 a_2 \dots a_n$:

1. Stack 1 is initially empty.
2. Stack 2 is filled with $a_1, a_2, \dots, a_n$ from top to bottom (so $a_1$ is on top), followed by infinitely many blanks, which we simulate by pushing a single blank symbol $\sqcup$ when needed.
3. The finite control of the 2-stack automaton stores the current DTM state, initially $q_0$.

### Simulating a DTM transition

Suppose the DTM is in state $q$ and the symbol under the head is $X$. A transition of $M$ has the form
\[
\delta(q, X) = (q', Y, D),
\]
where $Y$ is the symbol written in place of $X$, and $D \in \{\text{L}, \text{R}\}$ is the direction to move the head.

In the 2-stack automaton:

- $X$ is at the top of stack 2. We pop $X$ from stack 2 and push $Y$ instead, so the top of stack 2 becomes $Y$.
- We update the control state from $q$ to $q'$.
- Then we simulate the head move $D$:

Case $D = \text{R}$: move right.

1. Pop the top of stack 2 (this is $Y$, the symbol now under the head).
2. Push $Y$ onto stack 1 (since that cell is now to the left of the head).
3. Now the new symbol under the head is the next symbol on the tape to the right, which is at the new top of stack 2.
4. If stack 2 is empty at this point, that means the DTM head is moving onto a blank cell; we simulate this by pushing $\sqcup$ onto stack 2 as the symbol under the head.

Case $D = \text{L}$: move left.

1. Pop the top of stack 1 (this is the symbol of the cell immediately left of the previous head position; if stack 1 is empty, we instead use the blank symbol $\sqcup$).
2. The symbol $Y$ we wrote at the old head position is now one cell to the right of the head, so we push $Y$ onto stack 2.
3. The popped symbol from stack 1 becomes the new symbol under the head, so we push it onto stack 2 as the new top.
4. Again, if stack 1 was empty, we treat that as having read $\sqcup$ to the left.

These operations use only the tops of the two stacks and a finite number of control states, so they are valid stack operations for a 2-stack automaton.

### Acceptance and rejection

The 2-stack automaton keeps track of the current DTM state in its finite control. When the DTM would enter $q_{\text{acc}}$, the automaton enters a corresponding accepting state and halts. When the DTM would enter $q_{\text{rej}}$, the automaton enters a rejecting (non-accepting) halting state.

Thus every step of the deterministic Turing machine is simulated exactly by a bounded number of moves of the 2-stack finite automaton, preserving the configuration (tape contents, head position, and control state).

Therefore, a finite-state automaton with two stacks can simulate any deterministic Turing machine.

