# Grover Search and Amplitude Amplification

## 1. Unstructured search

Suppose a predicate marks \(M\) solutions among \(N\) possible items. Classically, unstructured search requires \(O(N/M)\) predicate evaluations in the worst-case scaling sense. Grover-type quantum search finds a marked item using

\[
O\!\left(\sqrt{\frac{N}{M}}\right)
\]

oracle calls.

For one marked item, this is \(O(\sqrt N)\).

## 2. Two-dimensional geometry

Define normalized superpositions over good and bad states,

\[
|G\rangle,
\qquad
|B\rangle.
\]

The uniform initial state can be written

\[
|s\rangle
=
\sin\theta|G\rangle
+
\cos\theta|B\rangle,
\]

where

\[
\sin^2\theta=\frac{M}{N}.
\]

The Grover iterate consists of two reflections: a phase flip on marked states and a reflection about the initial state. Their product is a rotation by \(2\theta\) in the span of \(|G\rangle,|B\rangle\).

After \(k\) iterations,

\[
G^k|s\rangle
=
\sin((2k+1)\theta)|G\rangle
+
\cos((2k+1)\theta)|B\rangle.
\]

Choosing \(k\approx \pi/(4\theta)\) gives high success probability.

## 3. Amplitude amplification

Grover search is a special case of amplitude amplification. If an initial algorithm succeeds with probability

\[
p=\sin^2\theta,
\]

coherent reflections can increase the good amplitude so that only \(O(1/\sqrt p)\) uses of the underlying procedure are required rather than \(O(1/p)\) independent repetitions.

## 4. What the speedup is—and is not

The improvement is quadratic in query complexity, not exponential. The full benefit depends on the cost of implementing the oracle and reflections. If checking a candidate is itself costly to make reversible or coherent, that cost must be included.

## 5. Optimality

Grover's quadratic query scaling is asymptotically optimal for black-box unstructured search. This makes it a clean example of a proven quantum advantage in a specified oracle model.

## References

1. L. K. Grover, "A fast quantum mechanical algorithm for database search," STOC 1996. https://doi.org/10.1145/237814.237866
2. C. H. Bennett et al., "Strengths and weaknesses of quantum computing," *SIAM J. Comput.* 26, 1510–1523 (1997). https://doi.org/10.1137/S0097539796300933
