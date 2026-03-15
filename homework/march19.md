A RAM has a finite program, a program counter, and registers $R_0, R_1, R_2, \ldots$ holding natural numbers. Typical instructions: load/store, add/subtract, jump, conditional jump, halt.

We simulate this RAM on a multi-tape Turing machine (which is equivalent to a single-tape TM):

- Use one tape (or a fixed number of tapes) to store the program and the program counter.
- Encode register contents on the tape, e.g. register $i$ holds $n$ by a block of the form #$i$#a<sup>$n$</sup># or by storing the pair $(i, n)$ in a list. With a suitable encoding, the tape alphabet is finite.

One step of the RAM (fetch instruction, decode, update registers and program counter) can be carried out by moving the TM head(s), rewriting symbols, and changing state. Each RAM instruction uses only finitely many TM steps. So the whole RAM computation is simulated step-by-step by the TM. Thus any function computable by a RAM is computable by a TM, and hence by a UTM (by giving it the encoding of that TM and the input).

A Turing machine has a finite set of states $Q$, tape alphabet $\Gamma$, transition function $\delta$, and an infinite tape. We simulate it on a RAM as follows:

- Store the tape as RAM memory: e.g. memory location $i$ holds the symbol at tape cell $i$ (encode symbols as numbers). Use two registers for the head position and the current state (encoded as a number).
- One step of the TM: read the symbol at the current head position from memory, look up $\delta(\text{state}, \text{symbol})$ (by conditional branches or a table in memory), write the new symbol to that cell, update the head position (add or subtract 1), and set the new state. Repeat until the TM halts.

So the RAM can mimic the TM’s configuration and transition function. Thus any function computable by a TM (and in particular by a UTM) is computable by a RAM.
