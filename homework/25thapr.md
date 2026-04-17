To show that there exists a function that is not time-constructible, consider the following reasoning.

Recall: A function \( f: \mathbb{N} \to \mathbb{N} \) is *time-constructible* if there is a Turing machine which, on input \( 1^n \), halts after exactly \( f(n) \) steps (for all sufficiently large \( n \)).

**Diagonalization Argument:**

Suppose toward contradiction that _every_ function \( f:\mathbb{N} \to \mathbb{N} \) is time-constructible. That means for every function, there is a corresponding Turing machine as above.

But, the set of Turing machines (and thus time-constructible functions) is *countable*, whereas the set of all functions \( f: \mathbb{N} \to \mathbb{N} \) is *uncountable* (by Cantor’s argument). 

Therefore, **most functions are not time-constructible**!

**Explicit Example:**

One can also construct a function that grows "faster than any time-constructible function," thus cannot be time-constructible itself (since it would contradict its own definition if it tried to construct itself).

For example, let \( \{f_i\} \) enumerate all time-constructible functions (since they are at most countable). Then define:

\[
g(n) = f_n(n) + 1
\]

By diagonalization, \( g \) cannot be equal to any \( f_i \). In fact, if \( g \) were time-constructible, it would appear somewhere on the list, leading to a contradiction.

**Conclusion:**  
Not only does there exist a function that is not time-constructible, but in fact, "almost all" functions (in the set-theoretic sense) are not time-constructible.