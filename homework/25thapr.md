To show that there exists a function that is not time-constructible, use the following reasoning.

Recall: A function $f: \mathbb{N} \to \mathbb{N}$ is time-constructible if there is a Turing machine which, on input $1^n$, halts after exactly $f(n)$ steps (for all sufficiently large $n$).

Suppose, towards contradiction, that every function $f : \mathbb{N} \to \mathbb{N}$ is time-constructible. Then for every function, there is a corresponding Turing machine as above.

However, the set of Turing machines (and hence, the set of time-constructible functions) is countable, whereas the set of all functions $f: \mathbb{N} \to \mathbb{N}$ is uncountable (by Cantor’s argument).

Therefore, use this cardinality argument to conclude that most functions are not time-constructible.

You can also use diagonalization to construct a function that is not time-constructible. List all time-constructible functions as $\{f_i\}$. Define:

$g(n) = f_n(n) + 1$


By diagonalization, $g$ cannot be equal to any $f_i$. Therefore, if $g$ were time-constructible, it would appear on the list, leading to a contradiction.