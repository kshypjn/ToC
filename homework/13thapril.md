To show that PATH is logspace-reducible to co-PATH, we need to give a logspace-computable function that, given an instance of PATH, creates an instance of co-PATH where the answer to the PATH instance is 'yes' if and only if the answer to the co-PATH instance is 'no'.

Recall:
- PATH = { (G, s, t) | there is a path from s to t in G }
- co-PATH = { (G, s, t) | there is no path from s to t in G }

Reduction:

Given an instance (G, s, t) of PATH, we use the same instance (G, s, t) as input to co-PATH.

- The logspace function f is: f(G, s, t) = (G, s, t)
- This is computable in logspace, since it just copies the input.

Correctness:

- If (G, s, t) is in PATH (there is a path from s to t), then (G, s, t) is not in co-PATH (there is not no path).
- If (G, s, t) is not in PATH (there is no path from s to t), then (G, s, t) is in co-PATH.

So this is a simple reduction and works in logspace.

Conclusion:

PATH is logspace-reducible to co-PATH with the function f(G, s, t) = (G, s, t).