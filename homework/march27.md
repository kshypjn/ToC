To prove a lower bound for sorting $n$ integers in the Turing machine model, consider the following.

Assume the input is $n$ numbers, each encoded in binary, and placed sequentially on the tape. Each number uses $O(\log N)$ bits if the numbers are at most $N$.

In the standard comparison-based model, any algorithm that sorts $n$ elements must perform at least $\Omega(n \log n)$ comparisons, since there are $n!$ possible orderings and each comparison gives at most one bit of information.

However, on a single-tape Turing machine, an extra cost comes from the tape's sequential access. To compare two numbers that are far apart, the machine must move its head between them, which could be up to $O(n \log N)$ steps for each comparison if the numbers are on opposite ends of the tape. Moving or copying numbers also takes time proportional to their distance.

If we think about sorting by repeatedly comparing and possibly moving items, then the time to sort is at least the number of required comparisons times the cost per comparison or rearrangement. For many reasonable sorting algorithms, this results in a time lower bound of $\Omega(n^2 \log N)$ on a single-tape Turing machine, since moving the head and modifying the tape is slow.

So the lower bound for sorting $n$ numbers in the single-tape Turing machine model is $\Omega(n^2 \log N)$. This reflects both the fundamental information-theoretic lower bound and the extra sequential-access cost of Turing machines.
