# Deutsch–Jozsa Algorithm

## 1. Why this algorithm matters

The Deutsch–Jozsa algorithm is one of the cleanest demonstrations of how a quantum algorithm can use **coherent oracle access, phase kickback, and interference** to extract a global property of a function.

Its practical importance is limited, but its conceptual importance is high: it teaches how to separate an algorithmic speedup from the assumptions of the oracle model in which that speedup is stated.

## 2. Learning objectives

After this chapter, you should be able to:

- state the Deutsch–Jozsa promise problem,
- distinguish deterministic, randomized, and quantum query complexity,
- derive phase kickback from the standard Boolean oracle,
- derive the final amplitude of each computational-basis state,
- prove why the all-zero outcome distinguishes the promised cases,
- explain where the apparent exponential separation comes from,
- and identify why the result is mainly pedagogical rather than a generic practical speedup.

## 3. The promise problem

We are given oracle access to a Boolean function

```math
f:\{0,1\}^n\rightarrow\{0,1\},
```

with the promise that exactly one of the following is true:

- **constant:** $f(x)$ is the same for every $x$;
- **balanced:** $f(x)=0$ for exactly half of the $2^n$ inputs and $f(x)=1$ for the other half.

The task is to decide which case holds.

The promise is essential. Without it, observing a few function values would not determine whether the function is globally constant or merely highly unbalanced.

## 4. Classical query complexity

For an **exact deterministic** classical algorithm, the worst case requires

```math
2^{n-1}+1
```

queries.

Why? After seeing the same output on $2^{n-1}$ distinct inputs, the function could still be either constant or balanced. One additional query forces a distinction.

Therefore the exact deterministic query complexity is exponential in $n$.

However, this is not the whole classical story. A randomized classical algorithm can sample a small number of random inputs. If two different outputs are ever observed, the function is balanced. If all observed outputs agree, the algorithm reports constant with some error probability.

After $k$ independent samples from a balanced function, the probability that all sampled outputs agree is at most

```math
2\left(\frac12\right)^k
=2^{1-k}.
```

Thus bounded-error randomized query complexity is only $O(1)$ for fixed confidence.

This is a crucial lesson:

> Deutsch–Jozsa gives an exponential separation from **exact deterministic classical query complexity**, not from every reasonable classical model.

## 5. The coherent oracle

The standard reversible oracle is

```math
U_f|x,y\rangle
=
|x,y\oplus f(x)\rangle.
```

The second register is necessary because a general Boolean function is not itself a reversible transformation of $x$.

Prepare the target qubit in

```math
|-\rangle
=
\frac{|0\rangle-|1\rangle}{\sqrt2}.
```

Then

```math
U_f|x\rangle|-\rangle
=
(-1)^{f(x)}|x\rangle|-\rangle.
```

### Derivation of phase kickback

Starting from

```math
|x\rangle|-\rangle
=
\frac{1}{\sqrt2}
|x\rangle\left(|0\rangle-|1\rangle\right),
```

we obtain

```math
U_f|x\rangle|-\rangle
=
\frac{1}{\sqrt2}
|x\rangle
\left(
|f(x)\rangle-|1\oplus f(x)\rangle
\right).
```

If $f(x)=0$, the target remains $|-\rangle$. If $f(x)=1$, its sign flips. Therefore

```math
U_f|x\rangle|-\rangle
=
(-1)^{f(x)}|x\rangle|-\rangle.
```

The function value has been converted into a **relative phase**.

## 6. The algorithm step by step

Initialize

```math
|0\rangle^{\otimes n}|1\rangle.
```

Apply Hadamards to all qubits:

```math
|0\rangle^{\otimes n}|1\rangle
\longmapsto
\frac{1}{\sqrt{2^n}}
\sum_x |x\rangle|-\rangle.
```

Apply the oracle:

```math
\frac{1}{\sqrt{2^n}}
\sum_x |x\rangle|-\rangle
\longmapsto
\frac{1}{\sqrt{2^n}}
\sum_x (-1)^{f(x)}|x\rangle|-\rangle.
```

Now apply $H^{\otimes n}$ to the input register.

The Walsh–Hadamard transform satisfies

```math
H^{\otimes n}|x\rangle
=
\frac{1}{\sqrt{2^n}}
\sum_z (-1)^{x\cdot z}|z\rangle,
```

where

```math
x\cdot z
=
\sum_{j=1}^n x_jz_j\pmod 2.
```

Therefore the amplitude of a basis state $|z\rangle$ becomes

```math
\alpha_z
=
\frac{1}{2^n}
\sum_x
(-1)^{f(x)+x\cdot z}.
```

In particular, for $z=0^n$,

```math
\alpha_{0^n}
=
\frac{1}{2^n}
\sum_x (-1)^{f(x)}.
```

## 7. Correctness proof

### Constant case

If $f(x)=0$ for all $x$,

```math
\alpha_{0^n}=1.
```

If $f(x)=1$ for all $x$,

```math
\alpha_{0^n}=-1.
```

Either way,

```math
P(0^n)=1.
```

### Balanced case

If $f$ is balanced, exactly half of the terms in

```math
\sum_x(-1)^{f(x)}
```

are $+1$ and half are $-1$. Hence

```math
\alpha_{0^n}=0
```

and therefore

```math
P(0^n)=0.
```

Thus the rule is exact:

```text
measure 0...0  -> constant
anything else -> balanced
```

with a single coherent oracle query.

## 8. Worked example: two input qubits

Let

```math
f(x_1x_2)=x_1.
```

This function is balanced. The post-oracle input state is

```math
\frac12
\left(
|00\rangle+|01\rangle-|10\rangle-|11\rangle
\right).
```

This factorizes as

```math
|-\rangle|+\rangle.
```

Applying $H\otimes H$ gives

```math
|1\rangle|0\rangle=|10\rangle.
```

Since the output is not $|00\rangle$, the algorithm identifies the function as balanced.

## 9. Resource accounting

At the abstract query level:

| Resource | Scaling |
|---|---:|
| Oracle queries | $1$ |
| Input qubits | $n$ |
| Target qubits | $1$ |
| Hadamards | $2n+1$ |
| Measurements | $n$ computational-basis bits |

But the oracle is treated as a black box. If $f$ is supplied as a classical program, constructing a reversible coherent implementation of $U_f$ may require substantial gates, ancillas, and uncomputation.

Therefore

```math
\text{query complexity}
\neq
\text{full circuit complexity}.
```

## 10. Where the quantum effect comes from

The algorithm does not read all $2^n$ function values. Instead, it performs three operations:

```text
coherent superposition
-> phase encoding of f(x)
-> global interference
```

The final measurement tests a particular Fourier coefficient of the phase pattern.

The relevant quantity is

```math
\frac{1}{2^n}
\sum_x(-1)^{f(x)},
```

which is $\pm1$ for constant functions and $0$ for balanced functions.

This is better understood as a structured interference computation than as “evaluating all inputs in parallel.”

## 11. Common misconceptions

### “The quantum computer evaluates all $2^n$ outputs and reads them.”

No. The oracle acts coherently on a superposition, but measurement does not reveal the list $\{f(x)\}_x$. Interference extracts one global property.

### “Deutsch–Jozsa proves an exponential practical speedup.”

Not in a general sense. The exponential separation is against exact deterministic classical query complexity under a promise problem.

### “One quantum oracle query means one ordinary function evaluation.”

Not necessarily. Coherent reversible oracle access can be much more demanding than an ordinary classical call.

## 12. Connections

Deutsch–Jozsa introduces ideas that recur throughout quantum algorithms:

- **phase kickback** appears in phase estimation;
- **Fourier structure** appears in Simon's and Shor's algorithms;
- **oracle accounting** is central to Grover search and amplitude estimation;
- **global properties from interference** are a recurring quantum-algorithm design pattern.

## 13. Exercises

### Conceptual

1. Why is the promise that $f$ is either constant or balanced essential?
2. Why does the target register use $|-\rangle$ rather than $|0\rangle$?
3. Explain why the algorithm does not reveal the values $f(x)$ individually.
4. Which classical baseline gives the famous exponential query separation?

### Computational

5. Prove directly that

```math
H^{\otimes n}|x\rangle
=
\frac{1}{\sqrt{2^n}}
\sum_z(-1)^{x\cdot z}|z\rangle.
```

6. For $n=2$, run the algorithm algebraically for

```math
f(x_1,x_2)=x_1\oplus x_2.
```

7. Show that a randomized classical algorithm using $k$ uniformly random queries has error probability at most $2^{1-k}$ on a balanced function if it reports “constant” only when all observed outputs agree.

### Research-oriented

8. Suppose a paper compares one coherent quantum query with one ordinary classical call to a complicated function. What additional assumptions would you inspect before accepting the comparison?
9. Give an example of how reversible oracle construction could dominate the nominal query complexity.
10. Explain why promise problems are useful for proving separations but may require care when translating them into practical applications.

## 14. Key takeaways

- Deutsch–Jozsa solves a promised global-property problem with one quantum oracle query.
- Its mechanism is phase kickback followed by interference.
- The exact deterministic classical query complexity is exponential, but bounded-error randomized classical sampling is much cheaper.
- The oracle-access model is part of the complexity statement.
- The algorithm is best viewed as a foundational lesson in quantum-algorithm design and resource accounting.

## References

1. D. Deutsch and R. Jozsa, "Rapid solution of problems by quantum computation," *Proceedings of the Royal Society A* 439, 553–558 (1992). https://doi.org/10.1098/rspa.1992.0167
2. M. A. Nielsen and I. L. Chuang, *Quantum Computation and Quantum Information*, Cambridge University Press.
3. J. Preskill, *Quantum Computation Lecture Notes*. https://www.preskill.caltech.edu/ph229/
