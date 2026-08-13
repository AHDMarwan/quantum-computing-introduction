# Quantum Reinforcement Learning

## 1. Reinforcement-learning setting

In reinforcement learning (RL), an agent interacts sequentially with an environment. At time \(t\), the agent observes a state or observation \(s_t\), chooses an action \(a_t\), receives reward \(r_t\), and updates its policy.

The objective is commonly the expected discounted return

\[
J(\pi)
=
\mathbb E_\pi
\left[
\sum_{t=0}^{\infty}\gamma^tr_t
\right].
\]

Quantum reinforcement learning asks how quantum information processing changes this framework.

## 2. Several meanings of “quantum RL”

The term can describe different settings:

1. a classical environment with a quantum policy/value model;
2. a quantum agent interacting with a classical interface;
3. a genuinely quantum environment with coherent interactions;
4. quantum speedups for RL subroutines under oracle access assumptions.

These settings should not be conflated.

## 3. Variational quantum policy

A policy can be represented by a PQC,

\[
\pi_{\boldsymbol\theta}(a|s)
=
\operatorname{Tr}
\left[E_a\rho_{\boldsymbol\theta}(s)\right],
\]

where \(E_a\) is a measurement effect associated with action \(a\).

The policy is trained using policy-gradient, actor–critic, or other RL machinery.

## 4. Quantum environments

A more intrinsically quantum setting occurs when states and actions are quantum operations. The agent may receive a quantum system, choose an instrument or control channel, and receive a future quantum state. This connects RL with quantum control and adaptive experiment design.

## 5. Coherent interaction models

Some theoretical quantum-learning-agent models allow coherent access to environment dynamics rather than forcing a classical measurement after every interaction. Such access can alter query complexity, but the physical interface assumptions must be made explicit.

## 6. Evaluation

Relevant questions include

- sample efficiency,
- interaction/query complexity,
- policy representation cost,
- circuit execution cost,
- robustness to stochastic rewards,
- and whether the environment is classical or quantum.

Beating a small classical policy network on a benchmark does not by itself demonstrate quantum RL advantage.

## References

1. V. Dunjko, J. M. Taylor, and H. J. Briegel, "Quantum-enhanced machine learning," *Phys. Rev. Lett.* 117, 130501 (2016). https://doi.org/10.1103/PhysRevLett.117.130501
2. V. Dunjko and H. J. Briegel, "Machine learning & artificial intelligence in the quantum domain," *Rep. Prog. Phys.* 81, 074001 (2018). https://doi.org/10.1088/1361-6633/aab406
