To prove that the 0-1 Knapsack problem is NP-complete, we follow two steps: (1) Show it is in NP, and (2) Show it is NP-hard.

---

### 1. 0-1 Knapsack is in NP

Recall the 0-1 Knapsack (decision) problem:

- **Input:** $n$ items, each with a weight $w_i > 0$ and value $v_i > 0$, capacity $W$, and target value $V$.
- **Question:** Is there a subset of the items whose total weight is at most $W$ and whose total value is at least $V$?

**Certificate:** A subset (set of indices) of items.

**Verification**: Given a certificate (a subset of items), in polynomial time we can:
- Compute the total weight and total value of the subset (both sums over at most $n$ elements).
- Check if total weight $\leq W$ and total value $\geq V$.

Thus, 0-1 Knapsack is in NP.

---

### 2. 0-1 Knapsack is NP-hard

We show this by reducing SUBSET-SUM to Knapsack.

#### SUBSET-SUM Problem:

- **Input:** $n$ positive integers $a_1, \ldots, a_n$, and a target $t$.
- **Question:** Is there a subset $S$ such that $\sum_{i \in S} a_i = t$?

SUBSET-SUM is known to be NP-complete.

#### Reduction:

Given a SUBSET-SUM instance ($a_1, \ldots, a_n$, $t$):

- For Knapsack, set for $i=1,\ldots,n$:
    - $w_i = a_i$ (each weight is the corresponding integer)
    - $v_i = a_i$ (each value is the same as its weight)
- Set capacity $W = t$
- Set target value $V = t$

**Claim:** There is a subset summing to $t$ in SUBSET-SUM iff there is a subset of items with total weight $\leq t$ and total value $\geq t$ in Knapsack.

**Proof of claim:**
- If $\sum_{i \in S} a_i = t$, then the corresponding subset has weight $t$ and value $t$, so accepted.
- If a subset has total weight $\leq t$ and total value $\geq t$: Since value = weight for each item, the only way for value to be $\geq t$ while weight is $\leq t$ is for weight = value = $t$.

Thus, a solution to this Knapsack instance gives a solution to the SUBSET-SUM instance and vice versa.

This reduction is polynomial in time.

---

## Conclusion

Since Knapsack is in NP and NP-hard, 0-1 Knapsack is NP-complete.