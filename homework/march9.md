fix an alphabet $\Sigma$ and pick an order on the symbols (like $0<1$ or $a<b<c$). the shortlex order $\le_{\text{sl}}$ on $\Sigma^*$ is:

- first by length which means shorter strings come first
- ties broken lexicographically - using the fixed symbol order

a shortlex enumerator $E$ for a language $L \subseteq \Sigma^*$ is a machine that prints out strings, and:

- it prints only strings in $L$
- it eventually prints every string in $L$
- it prints them in shortlex order, without repeats

$$x_0 <_{\text{sl}} x_1 <_{\text{sl}} x_2 <_{\text{sl}} \cdots$$

and $\{x_0, x_1, x_2, \ldots\} = L$.

now to build a decider for $L$, just run the enumerator until it either prints $w$ (so we accept) or it prints something past $w$ in shortlex order (so we know $w$ will never show up).

on input $w$:

1. simulate $E$ step by step.
2. whenever $E$ prints a string $y$:
   - if $y = w$, accept
   - if $y >_{\text{sl}} w$, reject
   - if $y <_{\text{sl}} w$, just keep going
3. if $E$ ever halts and we never saw $w$, reject

this is all doable on a tm because we can compare $y$ and $w$ in shortlex order: compare lengths, and if equal compare lexicographically.


fix the input $w$.

look at all strings that come before (or equal to) $w$ in shortlex:

$$S = \{x \in \Sigma^\* : x \le_{\text{sl}} w\}.$$

this set is finite, because it’s contained in the set of strings of length $\le |w|$, and there are only finitely many of those.

now consider what the enumerator $E$ does. there are two cases:

- case 1: $w \in L$. then $E$ outputs $w$ at some finite time (since $E$ enumerates all of $L$). when that happens, $D$ accepts and halts.

- case 2: $w \notin L$. then $E$ will never output $w$.
  - if $E$ halts after finitely many outputs, then $D$ rejects in step 3, so it halts.
  - if $E$ keeps printing forever, it prints strings in strictly increasing shortlex order. but there are only finitely many strings in $S$, so $E$ can’t stay inside $S$ forever. eventually it must print some string $y$ with $y >_{\text{sl}} w$, and then $D$ rejects right away, so it halts.

so in all cases, $D$ halts on every input.

- if $D$ accepts, it must have seen $E$ print $w$. since $E$ prints only strings from $L$, we get $w \in L$.

- if $D$ rejects, either:
  - $E$ halted without printing $w$, so $w \notin L$ (because $E$ printed all of $L$), or
  - $E$ printed some $y >_{\text{sl}} w$ before ever printing $w$. but since $E$ prints in increasing shortlex order, once it prints something bigger than $w$, it will never go back and print $w$ later. so $w$ can’t be in $L$.

thus $L(D)=L$, and since $D$ halts on all inputs, $L$ is recursive.
