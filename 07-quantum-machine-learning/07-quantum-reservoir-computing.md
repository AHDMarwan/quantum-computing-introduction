# Quantum Reservoir Computing

## 1. Reservoir computing changes what is trained

Reservoir computing separates a complicated dynamical feature map from a simple trainable readout.

Instead of training all internal dynamics, one uses a fixed dynamical system—the **reservoir**—to transform an input sequence into a high-dimensional trajectory of observable features.

Only the readout is typically trained.

Quantum reservoir computing (QRC) uses a quantum system as this dynamical substrate.

## 2. Learning objectives

After this chapter, you should be able to:

- define a reservoir-computing pipeline,
- distinguish QRC from variational QML,
- formulate input injection and quantum state evolution,
- explain fading memory and nonlinear feature generation,
- define a linear readout model,
- distinguish temporal memory from quantum coherence time,
- analyze measurement overhead,
- compare quantum and classical reservoirs fairly,
- and identify when physical quantum dynamics provide a useful computational substrate.

## 3. Sequential learning problem

Let

```math
u_1,u_2,\ldots,u_T
```

be an input sequence.

A temporal learning task may predict

```math
y_t
=
F(u_t,u_{t-1},u_{t-2},\ldots).
```

Examples include:

- time-series forecasting,
- nonlinear system identification,
- delayed signal reconstruction,
- sequence classification,
- control.

A useful model must retain enough history while continually processing new inputs.

## 4. Generic QRC state update

Let the reservoir state at time $t$ be

```math
\rho_t.
```

An input-dependent quantum channel updates it:

```math
\rho_{t+1}
=
\mathcal E_{u_t}(\rho_t).
```

A unitary special case is

```math
\rho_{t+1}
=
U(u_t)\rho_tU^\dagger(u_t).
```

More general reservoirs may include dissipation:

```math
\rho_{t+1}
=
\mathcal E
\left[
U(u_t)\rho_tU^\dagger(u_t)
\right].
```

Open-system dynamics can be useful rather than merely harmful because controlled forgetting is necessary for fading memory.

## 5. Input injection

Input can enter through several mechanisms:

```text
rotation angles
Hamiltonian fields
ancilla-state injection
reset of selected qubits
measurement-conditioned control
continuous driving.
```

For example,

```math
U_{\mathrm{in}}(u_t)
=
e^{-iu_t Z_1}.
```

The input perturbs the reservoir, and internal interactions spread this perturbation into many degrees of freedom.

## 6. Fixed internal dynamics

A reservoir can evolve under a fixed Hamiltonian

```math
U_R
=
e^{-iH_R\Delta t}.
```

Then one step may be

```math
\rho_{t+1}
=
U_R
U_{\mathrm{in}}(u_t)
\rho_t
U_{\mathrm{in}}^\dagger(u_t)
U_R^\dagger.
```

The parameters of $H_R$ need not be trained.

This is the main difference from a VQC:

```text
VQC:
train internal quantum parameters

QRC:
usually keep internal quantum dynamics fixed
and train a simpler readout.
```

## 7. Observable feature vector

The quantum state is not directly accessible as a classical vector.

The reservoir is read through observables

```math
O_1,\ldots,O_m.
```

Define features

```math
z_{t,j}
=
\mathrm{Tr}(O_j\rho_t).
```

The classical feature vector is

```math
\mathbf z_t
=
(z_{t,1},\ldots,z_{t,m}).
```

The learning algorithm sees these measured features, not the full density matrix.

## 8. Linear readout

A common readout is

```math
\hat y_t
=
\mathbf w^T\mathbf z_t+b.
```

Weights are trained classically, often using ridge regression:

```math
\mathbf w_*
=
\arg\min_{\mathbf w}
\sum_t
(y_t-\mathbf w^T\mathbf z_t)^2
+
\lambda\|\mathbf w\|^2.
```

This optimization is convex and inexpensive compared with training a deep PQC.

## 9. Where nonlinearity comes from

The quantum state evolution is linear in density-matrix space, but the input-output map can be nonlinear in the classical input sequence because:

- input values parameterize nonlinear trigonometric gates,
- multiple inputs interact through recurrent quantum dynamics,
- measured observables contain products/interference of amplitudes,
- classical readout can combine many dynamical features.

Reservoir computing does not require training nonlinear hidden-layer weights.

## 10. Memory

A temporal reservoir must retain information about past inputs.

Conceptually,

```math
\rho_t
=
\mathcal F(u_{t-1},u_{t-2},\ldots).
```

If two input histories differing far in the past always produce identical present states, that information has been forgotten.

If the reservoir never forgets old information, it may also fail to respond stably to new streams.

Useful temporal processing therefore requires a balance between memory and forgetting.

## 11. Fading memory

A system has a fading-memory property when the influence of sufficiently old inputs decreases over time.

Schematically, if two sequences agree over a recent window, their current reservoir states become close even if their distant histories differ.

Dissipation can support this behavior by contracting state differences.

Thus in QRC,

```math
\text{some dissipation}
```

can improve computational stability.

## 12. Echo-state intuition

Classical reservoir computing often requires an echo-state-like property: asymptotically, the reservoir state should be determined primarily by the input history rather than arbitrary initial conditions.

A quantum analogue can be studied through contraction of channels:

```math
\|\rho_t-\sigma_t\|_1
\longrightarrow
0
```

for different initial states driven by the same sufficiently long input sequence.

This gives an operational way to study initialization forgetting.

## 13. Memory versus coherence time

These terms should not be confused.

### Physical coherence time

How long quantum phase information survives hardware noise.

### Computational memory

How long past input information affects the observable features relevant to the task.

A reservoir can retain useful classical temporal memory even when some microscopic coherence has decayed.

Conversely, a long-lived coherent state need not provide useful task memory.

## 14. Nonlinear memory capacity

Reservoir benchmarks often ask whether current outputs can reconstruct functions of delayed inputs, such as

```math
u_{t-k}
```

or nonlinear combinations

```math
u_{t-k}u_{t-l}.
```

A reservoir may trade linear memory for nonlinear processing capacity.

The ideal balance depends on the task.

## 15. Spatial multiplexing

One can combine observables from multiple physical subsystems or multiple reservoirs:

```math
\mathbf z_t
=
\left(
\mathbf z_t^{(1)},
\mathbf z_t^{(2)},
\ldots
\right).
```

This enlarges the readout feature space without necessarily training new internal quantum parameters.

The resource cost appears instead in hardware size and measurement count.

## 16. Temporal multiplexing

Between two input injections, one can sample observables at several intermediate times:

```math
t+	au_1,
\ldots,
t+	au_K.
```

These virtual nodes enlarge the effective feature vector.

This is useful but increases measurement and experimental timing complexity.

## 17. Worked example: one-qubit reservoir

Consider a single qubit with update

```math
\rho_{t+1}
=
R_x(\alpha)
R_z(u_t)
\rho_t
R_z^\dagger(u_t)
R_x^\dagger(\alpha).
```

Read out

```math
z_t
=
\langle Z\rangle_t.
```

Even this simple recurrent system creates a nonlinear temporal function of the input sequence because each new $R_z(u_t)$ acts on a state determined by previous inputs.

However, one qubit has limited memory and feature dimension, so richer reservoirs use interacting many-body systems or additional virtual nodes.

## 18. Interacting-spin reservoirs

A many-body reservoir may evolve under

```math
H
=
\sum_{i<j}J_{ij}X_iX_j
+
\sum_i h_iZ_i.
```

Input is injected into one or more sites, and observables across the system are measured.

Interactions distribute local input information into nonlocal correlations.

Disorder can create a rich spectrum of dynamical timescales.

## 19. Open-system reservoirs

A reservoir update can be a Lindblad-generated channel or other dissipative process.

In continuous time,

```math
\frac{d\rho}{dt}
=
-i[H,\rho]
+
\sum_k
\left(
L_k\rho L_k^\dagger
-
\frac12
\{L_k^\dagger L_k,\rho\}
\right).
```

Hamiltonian terms generate coherent mixing, while dissipators control relaxation and forgetting.

This gives a natural design space for memory/nonlinearity tradeoffs.

## 20. Measurement disturbance

Repeatedly measuring a quantum reservoir can disturb its state.

Experimental protocols therefore must specify whether features are obtained through:

- repeated identical reservoir runs,
- weak or nondestructive measurements,
- separate copies,
- destructive measurements followed by restart.

This can dramatically change physical runtime.

The abstract formula

```math
z_{t,j}=\mathrm{Tr}(O_j\rho_t)
```

hides the measurement protocol needed to estimate it.

## 21. Shot cost

If $m$ observables are estimated with $S$ shots each at $T$ time points, naive measurement cost scales as

```math
O(mST).
```

If the entire trajectory must be rerun for each destructive measurement, the physical execution cost can be substantially larger.

Thus measurement complexity is often a central QRC resource.

## 22. Physical reservoir computing

Candidate platforms include:

- interacting nuclear spins,
- superconducting circuits,
- neutral atoms,
- photonic systems,
- spin ensembles.

In physical reservoir computing, imperfections and native dynamics can become part of the computational substrate rather than something that must be digitally compiled away.

This creates a hardware-algorithm co-design perspective.

## 23. Training cost versus hardware characterization

QRC has little internal parameter optimization, but one still needs to characterize useful readout features and choose operating regimes.

Hyperparameters can include:

- input injection strength,
- evolution time,
- measured observables,
- dissipation rate,
- reservoir size.

Searching these hyperparameters is a real optimization cost even when the quantum Hamiltonian itself is fixed.

## 24. Classical reservoir baselines

Relevant baselines include:

- echo-state networks,
- liquid-state machines,
- recurrent neural networks,
- random recurrent features,
- delay-coordinate models,
- nonlinear autoregressive models.

Fair comparison should match:

```text
number of measured/readout features
training samples
physical time per input
readout model complexity
energy/hardware resources when relevant.
```

## 25. Quantum feature dimension is not automatically accessible

An $n$-qubit reservoir evolves in operator space of dimension up to

```math
4^n.
```

But the learner only accesses the observables actually measured.

If only $n$ local $Z$ expectations are measured, the classical readout has only $n$ direct features per time sample.

Thus

```math
\text{large quantum operator space}
\not\Rightarrow
\text{exponentially many accessible features}.
```

## 26. Advantage questions

Possible QRC advantages include:

- richer temporal feature maps per physical degree of freedom,
- favorable memory/nonlinearity tradeoff,
- compact hardware realization of useful dynamics,
- learning directly from quantum signals,
- lower training complexity because only the readout is optimized.

But these must be compared against strong classical reservoirs.

## 27. QRC with quantum inputs

A particularly natural setting is when the input at time $t$ is itself a quantum system.

The reservoir can interact coherently with the incoming state before measurement.

This avoids encoding a classical scalar and may preserve information that classical measurement preprocessing would destroy.

Quantum-native sequential data are therefore a promising setting for QRC research.

## 28. Relation to recurrent QNNs

Both QRC and recurrent QNNs maintain state across time.

The difference is mainly what is trained:

```text
QRC:
fixed internal dynamics + trained readout

recurrent QNN:
trainable internal dynamics and/or readout.
```

There is a continuum between these extremes.

## 29. Relation to dynamical systems and system identification

A reservoir can be viewed as a nonlinear state-space feature map.

QRC therefore connects machine learning with:

- dynamical systems,
- control theory,
- observability,
- system identification,
- open quantum systems.

This makes it broader than a circuit-architecture niche.

## 30. Common misconceptions

### “The quantum reservoir must be trained internally.”

Not in standard reservoir computing; fixed dynamics are a defining attraction.

### “Long coherence time automatically means good memory.”

No. Computational memory is task- and readout-dependent.

### “The full $4^n$ operator space becomes an accessible classical feature vector.”

No. Measurement limits which features are actually available.

### “Noise always hurts QRC.”

Excess noise destroys information, but controlled dissipation can support fading memory and stable dynamics.

### “Less quantum training automatically means lower total cost.”

Measurement, trajectory repetition, hardware characterization, and readout collection can dominate.

## 31. Exercises

### Conceptual

1. Distinguish QRC from a variational recurrent QNN.
2. Explain why some forgetting is necessary for stable reservoir computing.
3. Why are physical coherence time and computational memory different quantities?
4. Why is measurement protocol central to QRC resource accounting?

### Computational

5. For a readout with $m=50$ observables, $T=1000$ time points, and $S=500$ shots per observable, estimate the naive shot count.
6. Write the ridge-regression normal-equation solution for a feature matrix $Z$ and targets $y$.
7. For a contractive channel satisfying

```math
\|\mathcal E(\rho)-\mathcal E(\sigma)\|_1
\le
\lambda\|\rho-\sigma\|_1,
```

with $0<\lambda<1$, derive the $k$-step contraction bound.
8. Explain qualitatively how increasing interaction strength could trade memory for nonlinear mixing.

### Research-oriented

9. Design a QRC benchmark where the input is a quantum time series rather than classical scalars.
10. Propose a measurement-efficient QRC readout using a smaller set of observables or randomized measurements.
11. How would you distinguish useful quantum dynamics from simply having a larger random feature model?
12. Formulate a trainable reservoir architecture where only dissipation rates, rather than unitary gates, are optimized.

## 32. Key takeaways

- QRC uses fixed quantum dynamics as a temporal feature map and usually trains only a classical readout.
- Inputs perturb a recurrent quantum state; measured observables become classical features.
- Useful reservoirs balance fading memory with nonlinear separation of input histories.
- Physical coherence time is not the same as computational memory.
- Open-system dynamics and controlled dissipation can be computational resources.
- Measurement access limits the effective feature dimension and can dominate runtime.
- Strong QRC claims require comparison with classical reservoir methods under matched feature, data, and runtime budgets.

## References

1. K. Fujii and K. Nakajima, "Harnessing disordered-ensemble quantum dynamics for machine learning," *Physical Review Applied* 8, 024030 (2017). https://doi.org/10.1103/PhysRevApplied.8.024030
2. K. Nakajima et al., "Boosting computational power through spatial multiplexing in quantum reservoir computing," *Physical Review Applied* 11, 034021 (2019). https://doi.org/10.1103/PhysRevApplied.11.034021
3. K. Nakajima, "Physical reservoir computing—an introductory perspective," *Japanese Journal of Applied Physics* 59, 060501 (2020). https://doi.org/10.35848/1347-4065/ab8d4f
