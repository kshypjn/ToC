prove that no weighted automaton over ℝ with alphabet Σ = {a} can compute the function:

$$f(a^n) = \frac{\lambda^n e^{-\lambda}}{n!}$$

where $\lambda > 0$ is a fixed parameter.

Step 1: Compute the generating function of the Poisson distribution.

$$F(z) = \sum_{n=0}^{\infty} \frac{\lambda^n e^{-\lambda}}{n!} z^n = e^{-\lambda} \sum_{n=0}^{\infty} \frac{(\lambda z)^n}{n!}$$

$$F(z) = e^{-\lambda} \cdot e^{\lambda z} = e^{\lambda(z-1)}$$

Step 2: Show that F(z) is not a rational function.

Suppose for contradiction that $F(z) = e^{\lambda(z-1)}$ is rational, 

$$e^{\lambda(z-1)} = \frac{P(z)}{Q(z)}$$

where P(z) and Q(z) are polynomials with no common factors.

Step 3: Apply properties of exponential functions.

Taking the derivative:

$$\lambda e^{\lambda(z-1)} = \frac{P'(z)Q(z) - P(z)Q'(z)}{Q(z)^2}$$

This gives:

$$\lambda \cdot \frac{P(z)}{Q(z)} = \frac{P'(z)Q(z) - P(z)Q'(z)}{Q(z)^2}$$

Simplifying:

$$\lambda P(z) Q(z) = P'(z)Q(z) - P(z)Q'(z)$$

Step 4

Let deg(P) = p and deg(Q) = q.

- Left side: deg(λPQ) = p + q
- Right side: deg(P'Q - PQ') ≤ max(p - 1 + q, p + q - 1) = p + q - 1

This gives us: p + q = p + q - 1

This is a contradiction! 

The only way to avoid this contradiction would be if both P and Q have degree 0 and they are constants, but then:

$$e^{\lambda(z-1)} = \frac{c_1}{c_2}$$

which is constant, contradicting the fact that the exponential function is non-constant.

