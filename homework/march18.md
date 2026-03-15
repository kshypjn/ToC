the Busy Beaver function $\mathrm{BB}(n)$ is the maximum number of $1$s that an $n$-state, 2-symbol Turing machine can print on the tape before halting, starting from a blank tape.

Consider all possible 1-state Turing machines. Since there is only 1 state, call it $A$. For the machine to halt, at least one transition must go to the halting state.

- The machine starts in state $A$ on a blank tape (all $0$s).
- On reading $0$ in state $A$, it can write either $0$ or $1$, move Left or Right, and go either to state $A$ or halt.
- On reading $1$ in state $A$, same options.

But the machine only gets one step: if it halts immediately, it prints at most $1$ symbol (if it writes $1$). If it continues (loops to $A$), it needs to halt eventually, or it runs forever and does not halt (so not counted in the Busy Beaver definition).

The best-achievable outcome is:
- On reading $0$, write $1$, move (L or R), and halt.

This produces a single $1$ on the tape before halting.

Therefore, $\boxed{\mathrm{BusyBeaver}(1) = 1}$.
