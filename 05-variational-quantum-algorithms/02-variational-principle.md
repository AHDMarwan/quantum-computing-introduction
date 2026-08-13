# Variational Principle and the Hybrid Quantum–Classical Loop

## 1. Generic variational structure

A VQA defines a cost

$$
C(\boldsymbol\theta)
$$

that is estimated using a quantum processor. A classical optimizer then proposes new parameters:

$$
\boldsymbol\theta_{t+1}
=
\mathcal O\big(\boldsymbol\theta_t,\widehat C_t,\widehat{\nabla C}_t,\ldots\big).
$$

The hats emphasize that quantities obtained from finite quantum measurements are statistical estimates.

## 2. Quantum role

A quantum device typically

1. prepares $|\psi(\boldsymbol\theta)\rangle$,
2. measures one or more observables,
3. returns samples or expectation estimates.

For an observable $H$,

$$
C(\boldsymbol\theta)
=
\langle\psi(\boldsymbol\theta)|H|\psi(\boldsymbol\theta)\rangle.
$$

## 3. Classical role

The classical controller handles parameter updates, stopping rules, constraints, and often grouping or postprocessing of measurement results. Thus “hybrid” is not a cosmetic description; the algorithm's state includes both quantum and classical information.

## 4. Variational principle

For a Hermitian Hamiltonian $H$ with ground energy $E_0$, every normalized trial state satisfies

$$
\langle\psi|H|\psi\rangle\ge E_0.
$$

Therefore minimizing the energy over an ansatz gives an upper bound to the ground-state energy:

$$
E_{\rm var}
=
\min_{\boldsymbol\theta}
\langle\psi(\boldsymbol\theta)|H|\psi(\boldsymbol\theta)\rangle
\ge E_0.
$$

This principle underlies VQE but not every VQA.

## 5. Where approximation enters

A VQA can fail because of several distinct errors:

$$
\text{total error}
\approx
\text{ansatz error}
+
\text{optimization error}
+
\text{sampling error}
+
\text{hardware error}.
$$

These sources should not be conflated. A good optimizer cannot fix an ansatz that excludes the solution; a perfect ansatz is not enough if gradients vanish or hardware noise dominates.

## 6. Why VQAs became prominent

VQAs were motivated partly by the possibility of using shorter circuits and classical feedback on noisy devices. However, “shorter than phase estimation” does not imply “practically advantageous.” Measurement overhead, trainability, optimizer scaling, and classical competition remain central open questions.

## References

1. M. Cerezo et al., "Variational quantum algorithms," *Nat. Rev. Phys.* 3, 625–644 (2021). https://doi.org/10.1038/s42254-021-00348-9
2. J. R. McClean et al., "The theory of variational hybrid quantum-classical algorithms," *New J. Phys.* 18, 023023 (2016). https://doi.org/10.1088/1367-2630/18/2/023023
