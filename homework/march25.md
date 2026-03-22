Given an arbitrary TM $M = (Q, \Sigma, \Gamma, \delta, q_0, q_{accept}, q_{reject})$ with $n = |Q|$ states and original tape alphabet $\Gamma$, we construct another TM $M'$ with **at most 13 states** and a (potentially much larger) tape alphabet $\Gamma'$ such that $L(M') = L(M)$.

#### Construction Steps

1. **Encoding the Original State in Tape Symbols:**
    - Introduce new tape symbols to encode the *control state* of $M$ as part of the tape alphabet.
    - For each symbol $a \in \Gamma$, and state $q \in Q$, we create a *marked version* of $a$, denoted $[a, q]$, meaning "the head is scanning $a$ and the control is $q$".
    - All other symbols are unmarked, representing ordinary tape cells.
    - At any moment, at most one cell on the tape is marked.

2. **State Reduction to a Small, Fixed Set:**
    - $M'$ has a fixed set of states to execute the following high-level actions:
        1. Scan left/right to find the marked cell (i.e., where the head of $M$ is).
        2. Change the marked cell according to $M$'s transition function (including changing the encoded state).
        3. Move the mark left/right to simulate head motion.
        4. Halt on accept/reject when reaching $q_{accept}$ or $q_{reject}$ encodings.
    - These actions can be broken down into a fixed sequence of subroutines, each requiring a small, constant number of states.
    - It is possible (and has been proven concretely) to perform all needed actions with **13 states** (see Shannon, 1956).

3. **Transition Simulation:**
    - To simulate $M$'s transition $\delta(q, a) = (q', b, D)$:
        - Find $[a, q]$ on the tape.
        - Replace it with $[b, q']$.
        - Move the marked symbol one cell left or right (depending on $D$), updating markup as needed.

4. **Tape Alphabet Growth:**
    - $\Gamma'$ now consists of all pairs $(a, q)$ for $a \in \Gamma$ and $q \in Q$, yielding $|\Gamma| \times |Q|$ marked symbols, plus the original set.



