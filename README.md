# Quantum-State-Preparation

This is the second mini-project for the quantum computing course at the Erdos Institute.

## The Problem

Write a Qiskit function that takes a $2^n$ dimensional vector, $\Psi \in \mathbb{C}^{2n}$, such that $\Vert \Psi\Vert_2 =1$, and outputs a circuit, U, such that 

$$U |0\rangle_n = \sum_{x=0}^{2^n-1} \Psi_x |x\rangle_n$$

The construction may use any number of ancillas, arbitrary 1-qubit gates and multi-controlled $R_z$ gates, (the number of controlled maybe arbitrarily large). No classical bit and measurements allowed. 

## The Solution

As explained in the lecture, the full problem can be divided into to sub problems. By noting that the complex amplitude can be written as magnitude times the phase $\Psi_x = |\Psi_x| e^{i\phi (x)}$, one has the two subproblems

### subproblem 1: 
$$ | |\Psi|\rangle = \sum_{x=0}^{2^n-1} |\Psi_x| |x\rangle _n $$

### subproblem 2:
$$ \tilde{U}_{\phi} |x\rangle = e^{i\phi(x)} |x\rangle $$

One first construct the quantum state with positive real amplitudes and then adjust the corresponding phase for each computational basis state.
