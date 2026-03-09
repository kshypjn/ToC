Let $A = \{\langle M \rangle \mid M \text{ is a DFA that does not accept any string containing an odd number of } 1\text{s}\}$. We want to show that $A$ is decidable. That means we must build a Turing machine $D$ that, on input $\langle M \rangle$, always halts and answers correctly whether $M$ has this property.

Intuitively, $M$ is in $A$ if for every string $w$ over its input alphabet, whenever $w$ has an odd number of $1$s, $M$ rejects $w$. Another way to phrase this is:
$
\langle M \rangle \in A \iff L(M) \subseteq \{ w \mid \text{$w$ has an even number of } 1\text{s} \}.
$
The key point is that $M$ is a DFA, and for DFAs we can effectively construct new DFAs and test emptiness of languages.

We use the following standard facts about DFAs:
1. Given two DFAs, we can construct a DFA for the intersection or difference of their languages.
2. Given a DFA, we can decide whether its language is empty by checking whether any accepting state is reachable from the start state (this can be done by a graph search).

Now define a DFA $E$ over the same alphabet as $M$ whose language is
\[
L(E) = \{ w \mid \text{$w$ has an odd number of } 1\text{s} \}.
\]
It is easy to build such a DFA: it just keeps track of parity (even vs odd) of the number of $1$s seen so far and accepts exactly the odd-parity state.

We want to check that $M$ rejects every string with an odd number of $1$s. Equivalently, we want to check that
\[
L(M) \cap L(E) = \emptyset.
\]
So we can construct a DFA $M'$ for the intersection $L(M') = L(M) \cap L(E)$ using the standard product construction for DFA intersection. This is an effective, mechanical procedure.

Our decider $D$ for $A$ works as follows on input $\langle M \rangle$:

1. Construct the DFA $E$ that recognizes all strings with an odd number of $1$s.
2. Construct the DFA $M'$ for the intersection $L(M') = L(M) \cap L(E)$ using the product construction.
3. Test whether $L(M')$ is empty:
   - Run a graph search (e.g., BFS or DFS) from the start state of $M'$.
   - If you ever reach an accepting state of $M'$, then $L(M') \neq \emptyset$.
4. If $L(M')$ is empty, then accept $\langle M \rangle$ (since $M$ never accepts a string with an odd number of $1$s). Otherwise, reject $\langle M \rangle$.

This procedure always halts because:
1. The constructions of $E$ and $M'$ are finite and algorithmic.
2. Emptiness testing for a DFA is just a finite graph search.

It is also correct:
1. If $M$ ever accepts some string with an odd number of $1$s, then that string is in $L(M) \cap L(E)$, so $L(M')$ is nonempty and we reject.
2. If $M$ never accepts any string with an odd number of $1$s, then $L(M) \cap L(E) = \emptyset$, so $L(M')$ is empty and we accept.

Therefore $D$ decides $A$, so $A$ is a decidable language.
