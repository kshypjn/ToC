Consider the tape of the Turing machine $M$ as a sequence of discrete cells. For any boundary between cell $i$ and cell $i+1$, a crossing sequence $C_i$ is defined as the ordered list of states that $M$ is in when its read/write head moves across this specific boundary. 

If $M$ halts on an input of length $n$, the sum of the lengths of all crossing sequences for the boundaries within the input portion of the tape is bounded by the total number of steps the machine takes:

$T(n) \ge \sum_{i=0}^{n} |C_i|$

We are given that $M$ runs in $O(n)$ time. Therefore, there exists a constant $c$ such that for all inputs of length $n$, the total running time is bounded by $c \cdot n$. 

Substituting this into our crossing sequence sum gives:

$\sum_{i=0}^{n} |C_i| \le c \cdot n$

This inequality implies that the average length of a crossing sequence across the input is bounded by the constant $c$. 

Because the Turing machine has a finite set of states $Q$, the number of possible crossing sequences of a given length is also finite. 


