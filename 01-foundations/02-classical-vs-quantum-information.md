# Classical vs Quantum Information

## 1. Why the distinction matters

Quantum information is not obtained by replacing a classical probability distribution with a more complicated probability distribution. The central difference is that quantum theory assigns **complex amplitudes** to alternatives, and probabilities appear only after a measurement rule is applied. Relative phase therefore affects future statistics even when two states have identical probabilities in a particular measurement basis.

## 2. Classical bits and probability distributions

A classical bit takes a definite value in

\[
\{0,1\}.
\]

If the value is uncertain, we use a probability distribution

\[
p=(p_0,p_1),\qquad p_0+p_1=1.
\]

For example, a fair random bit has

\[
p_0=p_1=\frac12.
\]

Classical randomness describes uncertainty about which alternative is realized. If a reversible classical transformation is applied, it permutes basis states. More general stochastic processes map probability distributions to probability distributions.

## 3. Quantum amplitudes

A pure qubit state is

\[
|\psi\rangle=\alpha|0\rangle+\beta|1\rangle,
\qquad |\alpha|^2+|\beta|^2=1.
\]

The coefficients \(\alpha,\beta\in\mathbb C\) are amplitudes. A computational-basis measurement gives

\[
P(0)=|\alpha|^2,\qquad P(1)=|\beta|^2.
\]

The phase is not visible in this measurement alone. Compare

\[
|+\rangle=\frac{|0\rangle+|1\rangle}{\sqrt2},
\qquad
|-\rangle=\frac{|0\rangle-|1\rangle}{\sqrt2}.
\]

Both produce \(0\) and \(1\) with probability \(1/2\) in the computational basis, but they are orthogonal states:

\[
\langle +|-\rangle=0.
\]

Applying a Hadamard gate reveals the difference:

\[
H|+\rangle=|0\rangle,
\qquad
H|-\rangle=|1\rangle.
\]

This is the simplest example of **interference**.

## 4. Superposition is not classical ignorance

The density operator for the pure state \(|+\rangle\) is

\[
|+\rangle\langle+|
=
\frac12
\begin{pmatrix}
1&1\\
1&1
\end{pmatrix}.
\]

The classical 50/50 mixture of \(|0\rangle\) and \(|1\rangle\) is

\[
\rho_{\mathrm{mix}}
=
\frac12|0\rangle\langle0|
+
\frac12|1\rangle\langle1|
=
\frac12 I.
\]

The diagonal probabilities are the same in the computational basis, but the off-diagonal terms of the coherent state preserve phase information. This distinction between coherence and classical uncertainty is fundamental.

## 5. Information is measurement-dependent

A quantum state does not carry a list of simultaneously accessible classical values. Which probability distribution is observed depends on the chosen measurement. Noncommuting observables generally cannot be assigned jointly sharp values in the same way as classical random variables.

This has several consequences:

- reading quantum information is an active physical process,
- measurement can disturb the state,
- incompatible measurements expose different features of the same state,
- and a state cannot generally be copied perfectly when it is unknown.

The no-cloning theorem follows from linearity. If a unitary cloned arbitrary states, then for two states \(|\psi\rangle\) and \(|\phi\rangle\), preservation of inner products would require

\[
\langle\psi|\phi\rangle
=
\langle\psi|\phi\rangle^2,
\]

which fails for generic nonorthogonal states.

## 6. Where quantum advantage can come from

The mere presence of a vector with \(2^n\) amplitudes does not yield an automatic computational speedup. Quantum algorithms must arrange amplitudes so that interference and measurement expose useful global information with fewer resources than a relevant classical procedure.

Possible resources include

- coherent superposition,
- phase and interference,
- entanglement,
- noncommuting observables,
- quantum memory,
- coherent oracle access,
- and direct access to quantum data.

The operational question is always: **what task is solved, under what input model, with what resource count, compared with what classical baseline?**

## 7. Key takeaway

A classical probability distribution contains probabilities. A pure quantum state contains amplitudes whose magnitudes determine probabilities and whose relative phases affect future interference. This distinction is the conceptual starting point for quantum algorithms and quantum machine learning.

## References

1. M. A. Nielsen and I. L. Chuang, *Quantum Computation and Quantum Information*, Cambridge University Press.
2. J. Watrous, *The Theory of Quantum Information*, 2018: https://cs.uwaterloo.ca/~watrous/TQI/
3. W. K. Wootters and W. H. Zurek, "A single quantum cannot be cloned," *Nature* 299, 802–803 (1982). https://doi.org/10.1038/299802a0
