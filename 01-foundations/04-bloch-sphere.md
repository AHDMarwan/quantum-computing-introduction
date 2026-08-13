# The Bloch Sphere

## 1. Why a sphere appears

A normalized pure qubit state has two complex amplitudes, but normalization removes one real degree of freedom and global phase removes another. Two real parameters remain. Therefore every pure qubit state can be written as

\[
|\psi\rangle
=
\cos\frac\theta2|0\rangle
+e^{i\phi}\sin\frac\theta2|1\rangle,
\]

with

\[
0\le\theta\le\pi,
\qquad
0\le\phi<2\pi.
\]

These angles identify a point on the unit sphere.

## 2. Bloch vector

The corresponding unit vector is

\[
\mathbf r
=
(\sin\theta\cos\phi,\,
 \sin\theta\sin\phi,\,
 \cos\theta).
\]

For a general single-qubit density operator,

\[
\rho
=
\frac12\left(I+\mathbf r\cdot\boldsymbol\sigma\right),
\]

where

\[
\boldsymbol\sigma=(X,Y,Z).
\]

Pure states satisfy

\[
\|\mathbf r\|=1,
\]

while mixed states satisfy

\[
\|\mathbf r\|<1.
\]

Thus pure states lie on the surface and mixed states lie inside the Bloch ball.

## 3. Important states

The poles are

\[
|0\rangle\leftrightarrow(0,0,1),
\qquad
|1\rangle\leftrightarrow(0,0,-1).
\]

The \(X\)-eigenstates are

\[
|+\rangle=\frac{|0\rangle+|1\rangle}{\sqrt2}
\leftrightarrow(1,0,0),
\]

\[
|-\rangle=\frac{|0\rangle-|1\rangle}{\sqrt2}
\leftrightarrow(-1,0,0).
\]

The \(Y\)-eigenstates are

\[
|+i\rangle=\frac{|0\rangle+i|1\rangle}{\sqrt2},
\qquad
|-i\rangle=\frac{|0\rangle-i|1\rangle}{\sqrt2}.
\]

## 4. Measurements as directions

For a state with Bloch vector \(\mathbf r\), the expectation values of the Pauli observables are

\[
\langle X\rangle=r_x,
\qquad
\langle Y\rangle=r_y,
\qquad
\langle Z\rangle=r_z.
\]

A projective measurement along a unit direction \(\mathbf n\) corresponds to the observable

\[
\mathbf n\cdot\boldsymbol\sigma.
\]

The probabilities of outcomes \(\pm1\) are

\[
p_\pm=\frac12(1\pm\mathbf r\cdot\mathbf n).
\]

## 5. Gates as rotations

A one-qubit unitary, up to a global phase, induces a rotation of the Bloch sphere. For example,

\[
R_x(\theta)=e^{-i\theta X/2}
\]

rotates the Bloch vector by angle \(\theta\) around the \(x\)-axis, and similarly for \(R_y\) and \(R_z\).

This geometric picture is useful for understanding single-qubit gates and parameterized circuits.

## 6. Limits of the picture

The Bloch sphere is a complete geometric representation only for a single qubit. A general two-qubit pure state has more degrees of freedom, and entanglement cannot be represented by simply drawing two independent Bloch vectors. Reduced Bloch vectors may even vanish for a maximally entangled state while the joint state remains pure.

For example, for

\[
|\Phi^+\rangle
=
\frac{|00\rangle+|11\rangle}{\sqrt2},
\]

each individual qubit has reduced state

\[
\rho_A=\rho_B=\frac I2,
\]

which lies at the center of the Bloch ball, even though the two-qubit state is pure.

## 7. Key takeaway

The Bloch sphere is the geometry of a single qubit: states are vectors in a ball, pure states lie on its surface, Pauli expectation values are Cartesian coordinates, and unitary gates act as rotations. It is powerful intuition, but multipartite quantum information requires the full tensor-product formalism.

## References

1. M. A. Nielsen and I. L. Chuang, *Quantum Computation and Quantum Information*.
2. J. Preskill, *Quantum Computation Lecture Notes*: https://www.preskill.caltech.edu/ph229/
