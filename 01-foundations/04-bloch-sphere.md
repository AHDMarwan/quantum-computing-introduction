# The Bloch Sphere

## 1. Why the Bloch sphere exists

A normalized pure qubit has two complex amplitudes,

```math
|\psi\rangle=\alpha|0\rangle+\beta|1\rangle,
```

but normalization removes one real degree of freedom and global phase removes another. Two real physical parameters remain. Therefore every pure qubit can be written as

```math
|\psi\rangle
=
\cos\frac\theta2|0\rangle
+
e^{i\phi}\sin\frac\theta2|1\rangle,
```

with

```math
0\le\theta\le\pi,
\qquad
0\le\phi<2\pi.
```

The pair $(\theta,\phi)$ is naturally represented by a point on the unit sphere.

The Bloch sphere is therefore not merely a visualization trick. It is the geometric representation of the projective state space of one pure qubit.

### Learning objectives

After this chapter, you should be able to:

- convert between state amplitudes and Bloch-sphere coordinates,
- derive the Bloch-vector representation of a density matrix,
- identify pure and mixed states geometrically,
- interpret Pauli expectation values as Cartesian coordinates,
- derive projective-measurement probabilities along arbitrary directions,
- understand one-qubit unitary gates as rotations,
- and recognize why the Bloch sphere does not generalize straightforwardly to entangled multiqubit states.

---

## 2. From amplitudes to spherical coordinates

Start from

```math
|\psi\rangle
=
\cos\frac\theta2|0\rangle
+
e^{i\phi}\sin\frac\theta2|1\rangle.
```

The corresponding Bloch vector is

```math
\mathbf r
=
\begin{pmatrix}
r_x\\
r_y\\
r_z
\end{pmatrix}
=
\begin{pmatrix}
\sin\theta\cos\phi\\
\sin\theta\sin\phi\\
\cos\theta
\end{pmatrix}.
```

For a pure state,

```math
\|\mathbf r\|=1.
```

Thus pure states lie on the surface of the unit sphere.

The computational basis states are the poles:

```math
|0\rangle\leftrightarrow(0,0,1),
```

```math
|1\rangle\leftrightarrow(0,0,-1).
```

---

## 3. Important states on the sphere

The eigenstates of $X$ are

```math
|+\rangle
=
\frac{|0\rangle+|1\rangle}{\sqrt2}
\leftrightarrow(1,0,0),
```

and

```math
|-\rangle
=
\frac{|0\rangle-|1\rangle}{\sqrt2}
\leftrightarrow(-1,0,0).
```

The eigenstates of $Y$ are

```math
|+i\rangle
=
\frac{|0\rangle+i|1\rangle}{\sqrt2}
\leftrightarrow(0,1,0),
```

and

```math
|-i\rangle
=
\frac{|0\rangle-i|1\rangle}{\sqrt2}
\leftrightarrow(0,-1,0).
```

These six states form the positive and negative coordinate-axis directions of the Bloch sphere.

---

## 4. Density matrices and the Bloch vector

A general one-qubit density operator can be expanded in the Pauli basis:

```math
\rho
=
\frac12
\left(
I+r_xX+r_yY+r_zZ
\right).
```

Equivalently,

```math
\rho
=
\frac12
\left(
I+\mathbf r\cdot\boldsymbol\sigma
\right),
```

where

```math
\boldsymbol\sigma=(X,Y,Z).
```

In matrix form,

```math
\rho
=
\frac12
\begin{pmatrix}
1+r_z&r_x-ir_y\\
r_x+ir_y&1-r_z
\end{pmatrix}.
```

The Bloch components can be recovered from expectation values:

```math
r_x=\mathrm{Tr}(\rho X),
```

```math
r_y=\mathrm{Tr}(\rho Y),
```

```math
r_z=\mathrm{Tr}(\rho Z).
```

Thus the Bloch vector is not only geometric; its coordinates are directly measurable observables.

---

## 5. Pure states and mixed states

For a one-qubit density matrix,

```math
\rho
=
\frac12(I+\mathbf r\cdot\boldsymbol\sigma).
```

Its purity is

```math
\mathrm{Tr}(\rho^2)
=
\frac12(1+\|\mathbf r\|^2).
```

A pure state satisfies

```math
\mathrm{Tr}(\rho^2)=1,
```

so

```math
\|\mathbf r\|=1.
```

A mixed state satisfies

```math
0\le\|\mathbf r\|<1.
```

Therefore:

```text
surface of sphere  → pure states
inside the sphere  → mixed states
center              → maximally mixed state I/2
```

At the center,

```math
\rho=\frac I2,
```

and

```math
\langle X\rangle
=
\langle Y\rangle
=
\langle Z\rangle
=0.
```

---

## 6. Deriving the density matrix of a pure Bloch state

For

```math
|\psi\rangle
=
\cos\frac\theta2|0\rangle
+
e^{i\phi}\sin\frac\theta2|1\rangle,
```

we have

```math
\rho
=|\psi\rangle\langle\psi|.
```

Expanding,

```math
\rho
=
\begin{pmatrix}
\cos^2(\theta/2)&
\cos(\theta/2)\sin(\theta/2)e^{-i\phi}\\
\cos(\theta/2)\sin(\theta/2)e^{i\phi}&
\sin^2(\theta/2)
\end{pmatrix}.
```

Using

```math
\cos^2\frac\theta2
=
\frac{1+\cos\theta}{2},
```

```math
\sin^2\frac\theta2
=
\frac{1-\cos\theta}{2},
```

and

```math
2\cos\frac\theta2\sin\frac\theta2
=
\sin\theta,
```

we obtain

```math
\rho
=
\frac12
\begin{pmatrix}
1+\cos\theta&
\sin\theta e^{-i\phi}\\
\sin\theta e^{i\phi}&
1-\cos\theta
\end{pmatrix}.
```

Since

```math
e^{i\phi}=\cos\phi+i\sin\phi,
```

this becomes exactly

```math
\rho
=
\frac12
\left(
I
+
\sin\theta\cos\phi\,X
+
\sin\theta\sin\phi\,Y
+
\cos\theta\,Z
\right).
```

This derives the Bloch vector directly from the state amplitudes.

---

## 7. Measurement as a direction on the sphere

Let $\mathbf n$ be a unit vector. The spin observable along that direction is

```math
M_{\mathbf n}
=
\mathbf n\cdot\boldsymbol\sigma.
```

Its eigenvalues are $+1$ and $-1$. The corresponding projectors are

```math
P_+
=
\frac12(I+\mathbf n\cdot\boldsymbol\sigma),
```

```math
P_-
=
\frac12(I-\mathbf n\cdot\boldsymbol\sigma).
```

For

```math
\rho
=
\frac12(I+\mathbf r\cdot\boldsymbol\sigma),
```

the probabilities are

```math
p_+
=
\mathrm{Tr}(\rho P_+)
=
\frac12(1+\mathbf r\cdot\mathbf n),
```

and

```math
p_-
=
\frac12(1-\mathbf r\cdot\mathbf n).
```

Therefore the measurement statistics depend only on the angle between the state vector and measurement direction.

If $\gamma$ is that angle,

```math
\mathbf r\cdot\mathbf n=\cos\gamma
```

for a pure state, so

```math
p_+=\cos^2\frac\gamma2,
```

```math
p_-=\sin^2\frac\gamma2.
```

This geometric form of the Born rule is one of the most useful single-qubit intuitions.

---

## 8. Pauli measurements

Measurement along the coordinate axes gives

```math
\langle X\rangle=r_x,
```

```math
\langle Y\rangle=r_y,
```

```math
\langle Z\rangle=r_z.
```

Hence measuring $X$, $Y$, and $Z$ on repeated copies of the same state is enough to reconstruct any one-qubit density matrix.

This is the simplest example of quantum-state tomography.

The reconstruction formula is

```math
\rho
=
\frac12
\left[
I
+\langle X\rangle X
+\langle Y\rangle Y
+\langle Z\rangle Z
\right].
```

---

## 9. One-qubit gates as rotations

Any one-qubit unitary can be written, up to a global phase, in the form

```math
U
=
e^{-i\theta\mathbf n\cdot\boldsymbol\sigma/2}.
```

On the Bloch sphere, this corresponds to a rotation of the Bloch vector by angle $\theta$ about axis $\mathbf n$.

For example,

```math
R_x(\theta)=e^{-i\theta X/2}
```

rotates around the $x$ axis,

```math
R_y(\theta)=e^{-i\theta Y/2}
```

rotates around the $y$ axis, and

```math
R_z(\theta)=e^{-i\theta Z/2}
```

rotates around the $z$ axis.

The state-vector transformation lives in the group $SU(2)$, while the Bloch-vector transformation is a three-dimensional rotation in $SO(3)$. The mapping is two-to-one: $U$ and $-U$ induce the same Bloch-sphere rotation because they differ only by a global phase on state vectors.

---

## 10. Worked example: locate a state on the Bloch sphere

Consider

```math
|\psi\rangle
=
\frac{1}{\sqrt3}|0\rangle
+
\sqrt{\frac23}e^{i\pi/4}|1\rangle.
```

Compare with

```math
|\psi\rangle
=
\cos\frac\theta2|0\rangle
+
e^{i\phi}\sin\frac\theta2|1\rangle.
```

We identify

```math
\cos\frac\theta2=\frac1{\sqrt3},
```

so

```math
\cos\theta
=
2\cos^2\frac\theta2-1
=
-\frac13.
```

Also,

```math
\phi=\frac\pi4.
```

Now

```math
\sin\theta
=
\sqrt{1-\cos^2\theta}
=
\frac{2\sqrt2}{3}.
```

Therefore

```math
r_x
=
\sin\theta\cos\phi
=
\frac23,
```

```math
r_y
=
\sin\theta\sin\phi
=
\frac23,
```

```math
r_z=-\frac13.
```

Thus

```math
\mathbf r
=
\left(
\frac23,
\frac23,
-\frac13
\right).
```

Check normalization:

```math
\|\mathbf r\|^2
=
\frac49+\frac49+\frac19
=1.
```

The state lies on the Bloch-sphere surface, as expected for a pure state.

---

## 11. Worked example: measurement along an arbitrary axis

Suppose

```math
\mathbf r=(0,1,0)
```

and we measure along

```math
\mathbf n
=
\frac1{\sqrt2}(1,1,0).
```

Then

```math
\mathbf r\cdot\mathbf n
=
\frac1{\sqrt2}.
```

Therefore

```math
p_+
=
\frac12
\left(
1+\frac1{\sqrt2}
\right),
```

and

```math
p_-
=
\frac12
\left(
1-\frac1{\sqrt2}
\right).
```

The result depends only on the geometric angle between state and measurement direction.

---

## 12. Mixed states as shrinking of the Bloch vector

Consider depolarization:

```math
\rho'
=
(1-p)\rho
+p\frac I2.
```

If

```math
\rho
=
\frac12(I+\mathbf r\cdot\boldsymbol\sigma),
```

then

```math
\rho'
=
\frac12
\left[
I+(1-p)\mathbf r\cdot\boldsymbol\sigma
\right].
```

Therefore

```math
\mathbf r'
=(1-p)\mathbf r.
```

Depolarizing noise contracts the Bloch sphere toward the origin. This is a simple geometric picture of loss of purity.

Different noise channels produce different affine transformations of the Bloch ball.

---

## 13. Why the Bloch sphere stops being enough

The Bloch sphere is a complete representation only for a single qubit.

A pure state of two qubits requires

```math
2\cdot4-2=6
```

independent real physical parameters, already more than can be encoded by two ordinary three-dimensional unit vectors without additional correlation information.

More importantly, entanglement is a property of the joint state.

For the Bell state

```math
|\Phi^+\rangle
=
\frac{|00\rangle+|11\rangle}{\sqrt2},
```

the reduced states are

```math
\rho_A=\rho_B=\frac I2.
```

Both local Bloch vectors vanish:

```math
\mathbf r_A=\mathbf r_B=0.
```

Yet the joint state is pure and maximally entangled. The missing information lives in correlations that cannot be represented by the individual local Bloch vectors.

---

## 14. Common misconceptions

### Misconception 1: "Every point inside the Bloch ball is a pure state."

No. Pure states lie only on the surface. Interior points are mixed states.

### Misconception 2: "The Bloch sphere is the physical sphere around a qubit."

No. It is an abstract state-space representation.

### Misconception 3: "A Bloch vector is the same thing as a state vector."

No. $|\psi\rangle$ lives in $\mathbb C^2$ and is defined modulo global phase. $\mathbf r$ is a real three-dimensional representation of the corresponding density operator.

### Misconception 4: "Two qubits are represented by two Bloch spheres."

Only their reduced local states are. The full joint state generally contains correlation and entanglement information that the two local vectors do not capture.

### Misconception 5: "Every unitary corresponds to a unique three-dimensional rotation."

The correspondence is two-to-one: $U$ and $-U$ induce the same Bloch-sphere rotation.

---

## 15. Connections to quantum computing and QML

The Bloch sphere is especially useful for:

- understanding single-qubit gates,
- visualizing data-encoding rotations,
- interpreting expectation-value readouts,
- analyzing single-qubit noise,
- understanding parameterized rotation gates,
- and detecting when a claimed geometric intuition cannot extend to many-qubit entangled systems.

In QML, many feature maps encode classical variables as rotation angles. The Bloch sphere gives an immediate geometric picture of such encodings for one qubit, but that intuition must be supplemented by tensor-product and many-body structure for larger models.

---

## 16. Exercises

### A. Conceptual

1. Why does a pure qubit have two real physical degrees of freedom?
2. What does the center of the Bloch ball represent?
3. Why are $\langle X\rangle$, $\langle Y\rangle$, and $\langle Z\rangle$ sufficient to reconstruct a one-qubit state?
4. Explain why the Bloch sphere cannot capture bipartite entanglement using only local vectors.
5. What is the physical meaning of the length $\|\mathbf r\|$?

### B. Computational

6. Find the Bloch vector of

```math
|\psi\rangle
=
\frac{|0\rangle-|1\rangle}{\sqrt2}.
```

7. Find the density matrix corresponding to

```math
\mathbf r=
\left(
\frac12,
0,
\frac12
\right).
```

Is the state pure or mixed?

8. For a state with

```math
\mathbf r
=
\left(
\frac1{\sqrt2},
0,
\frac1{\sqrt2}
\right),
```

compute the probabilities of $Z$ measurement outcomes.

9. Show that $R_z(\pi)$ maps the Bloch vector $(1,0,0)$ to $(-1,0,0)$.
10. A qubit has measured expectation values

```math
\langle X\rangle=0.3,
\qquad
\langle Y\rangle=0.4,
\qquad
\langle Z\rangle=0.5.
```

Construct $\rho$ and compute its purity.

### C. Research-oriented

11. Why can a highly entangled many-qubit state have completely uninformative local Bloch vectors?
12. How might local Bloch-vector diagnostics miss important trainability or correlation structure in a QML model?
13. Compare angle encoding on one qubit with an encoding distributed over many qubits. What information does the single-qubit geometric picture fail to show?
14. Describe geometrically what a depolarizing channel does, then explain why more general channels need not be isotropic contractions.

---

## 17. Key takeaways

- The Bloch sphere is the complete state-space geometry of one qubit.
- Pure states lie on the sphere; mixed states lie inside the Bloch ball.
- The Bloch-vector coordinates are Pauli expectation values.
- Projective measurement along a direction $\mathbf n$ depends on $\mathbf r\cdot\mathbf n$.
- One-qubit unitaries act as rotations of the Bloch vector.
- Local Bloch vectors do not capture general multipartite correlations or entanglement.

---

## References

1. J. Preskill, *Lecture Notes for Physics 229: Quantum Information and Computation*, California Institute of Technology: https://www.preskill.caltech.edu/ph229/
2. J. Watrous, *The Theory of Quantum Information*, Cambridge University Press, 2018: https://cs.uwaterloo.ca/~watrous/TQI/
3. M. A. Nielsen and I. L. Chuang, *Quantum Computation and Quantum Information*, Cambridge University Press, 2010.
