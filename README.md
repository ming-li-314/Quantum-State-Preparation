# Quantum-State-Preparation

This is the second mini-project for the quantum computing course at the Erdos Institute.

## The Problem

Write a Qiskit function that takes a $2^n$ dimensional vector, $\Psi \in \mathbb{C}^{2n}$, such that $\Vert \Psi\Vert_2 =1$, and outputs a circuit, U, such that 

$$U |0\rangle_n = \sum_{x=0}^{2^n-1} \Psi_x |x\rangle_n$$

The construction may use any number of ancillas, arbitrary 1-qubit gates and multi-controlled $R_z$ gates, (the number of controlled maybe arbitrarily large). No classical bit and measurements allowed. 

## The Solution

As explained in the lecture, the full problem can be divided into two subproblems. By noting that the complex amplitude can be written as the magnitude times the phase $\Psi_x = |\Psi_x| e^{i\phi (x)}$, one has the two subproblems

### subproblem 1: 
$$ | |\Psi|\rangle = \sum_{x=0}^{2^n-1} |\Psi_x| |x\rangle _n $$

### subproblem 2:
$$ \tilde{U}_{\phi} |x\rangle = e^{i\phi(x)} |x\rangle $$

One first constructs the quantum state with positive real amplitudes and then adjust the corresponding phase for each computational basis state.


The subproblem 1 can be solved by recursion. For $n=1$,  $|\Psi > = a |0\rangle + b|1\rangle$, which can be obtained by applying the $R_y(\theta_0)$ gate on qubit $|0\rangle$ with $\theta_0 = 2\cos^{-1}{\left(a/\sqrt{a^2+b^2}\right)}$. 

$$ |\Psi\rangle_{n+1} = |\Psi_0\rangle_n \left(\cos{(\theta_0/2)} |0\rangle \right) + |\Psi_1 \rangle_n \left(\sin{(\theta_0/2)} |1\rangle \right) $$

If we denote the circuits to generate the quantum states $|\Psi_0\rangle$ and $|\Psi_1\rangle$ are $U_{\psi_0}$ and $U_{\psi_1}$, respectively. The circuit to generate the state $|\Psi\rangle_{n+1}$ can be schematically shown in the diagram. 
<img src="https://github.com/user-attachments/assets/5ab5af93-9dba-4ae5-9bd8-f281c32716ce"  width="400" height="200" />

This will be implemented recursively.

The subproblem 2 can be solved iteratively by using multi-controlled phase gate to add the corresponding phase to each computational basis state. 

### Implementation in the Jupyter notebook

In the Jupyter notebook, I implement two functions to solve subproblem 1 and subproblem 2 separately. These two functions are combined to solve the full problem.

I directly used multi-controlled $R_y$ gate and multi-controlled Phase gate from qiskit. This deviates from the requirement that only multi-controlled $R_z$ gate is allowed. I find it easier to use multi-controlled phase gate to directly adjust the phases in subproblem 2 than using multi-controlled $R_z$ gate because the latter will introduce global phases that need to be carefully removed. 



### Analysis of Complexities and Resources
For $n$ qubits and total $N= 2^n$ amplitudes.

|Metric              |Complexity          |
|--------------------|--------------------|
|Number of Ancillas  |$0$              |
|Gate Count          |$O(2^n\cdot n)$              |
|Gate Depth          |$O(2^n \cdot n)$              |

The complexity and resource analysis is dominated by the subproblem 2 in which one needs to adjust the phases for the $2^n$ computational basis state. 
