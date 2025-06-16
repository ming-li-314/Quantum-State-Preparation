# Quantum-State-Preparation

This is the second mini-project for the quantum computing course at the Erdos Institute

## The Problem

Write a Qiskit function that takes a $2^n$ dimensional vector, $\Psi \in \mathbb{C}^{2n}$, such that $\Vert \Psi\Vert_2 =1$, and outputs a circuit, U, such that 

$$U |0\rangle_n = \sum_{x=0}^{2^n-1} \Psi_x |x\rangle_n$$

The construction may use any number of ancillas, arbitrary 1-qubit gates and multi-controlled $R_z$ gates, (the number of controlled maybe arbitrarily large). No classical bit and measurements allowed. 

## The Solution


