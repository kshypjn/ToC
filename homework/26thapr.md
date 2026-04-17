To show that $\mathrm{SPACE}(n) \neq \mathrm{SPACE}(n^2)$, we will use the Space Hierarchy Theorem.

The Space Hierarchy Theorem states:  
If $s_1(n)$ and $s_2(n)$ are space-constructible functions and $s_1(n) = o(s_2(n))$, then:
$\mathrm{DSPACE}(s_1(n)) \subsetneq \mathrm{DSPACE}(s_2(n))$
That is, there exist languages that can be decided in $O(s_2(n))$ space but not in $O(s_1(n))$ space (even up to constant factors).

Let's apply this to $s_1(n) = n$ and $s_2(n) = n^2$.

1. Both $n$ and $n^2$ are space-constructible functions. (A function $f(n)$ is space-constructible if there exists a Turing machine which, on input of size $n$, uses exactly $f(n)$ space up to constants.)

2. Clearly, $n = o(n^2)$.

Therefore, by the Space Hierarchy Theorem:
$\mathrm{DSPACE}(n) \subsetneq \mathrm{DSPACE}(n^2)$
or, equivalently,
$\mathrm{SPACE}(n) \neq \mathrm{SPACE}(n^2)$

There exist languages decidable in $O(n^2)$ space but not in $O(n)$ space. Thus,
$\mathrm{SPACE}(n) \neq \mathrm{SPACE}(n^2)$

In other words: Increasing the available space from linear to quadratic strictly increases the class of problems that can be solved by a Turing machine.