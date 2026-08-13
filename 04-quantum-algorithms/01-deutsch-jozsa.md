# Deutsch–Jozsa Algorithm

## 1. Problem

Given oracle access to a Boolean function

$$
f:\{0,1\}^n\rightarrow\{0,1\},
$$

promised to be either **constant** or **balanced**, determine which case holds.

A balanced function returns 0 on exactly half of its inputs and 1 on the other half.

## 2. Oracle

The standard coherent oracle is

$$
U_f|x,y\rangle
=
|x,y\oplus f(x)\rangle.
$$

Preparing the target qubit in

$$
|-\rangle=\frac{|0\rangle-|1\rangle}{\sqrt2}
$$

produces phase kickback:

$$
U_f|x\rangle|-\rangle
=(-1)^{f(x)}|x\rangle|-\rangle.
$$

Thus function values become relative phases.

## 3. Algorithm

Start from

$$
|0\rangle^{\otimes n}|1\rangle.
$$

Apply Hadamards, query $U_f$, then apply $H^{\otimes n}$ again to the input register.

Immediately before the final measurement, the amplitude of $|0^n\rangle$ is

$$
\frac{1}{2^n}
\sum_{x\in\{0,1\}^n}
(-1)^{f(x)}.
$$

If $f$ is constant, the magnitude is 1. If $f$ is balanced, the positive and negative terms cancel exactly, so the amplitude is 0.

Therefore a single oracle query distinguishes the two promised cases exactly.

## 4. What the algorithm teaches

Deutsch–Jozsa is more important pedagogically than practically. It illustrates

- coherent oracle access,
- phase kickback,
- global interference,
- and the distinction between deterministic classical query complexity and quantum query complexity under a promise.

It does **not** imply that an arbitrary classical function can be globally analyzed after one inexpensive real-world evaluation. The oracle model is part of the problem statement.

## References

1. D. Deutsch and R. Jozsa, "Rapid solution of problems by quantum computation," *Proc. R. Soc. A* 439, 553–558 (1992). https://doi.org/10.1098/rspa.1992.0167
