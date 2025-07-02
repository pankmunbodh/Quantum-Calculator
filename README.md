In this notebook, we implement the most basic functions of a Quantum Calculator : addition and multiplication. The quantum calculator uses a quantum circuit to implement these operations without resorting to any kind of classical logic or classical information processing.

Concretely, we write a Qiskit function that takes a positive integer $d$ as input and outputs a quantum circuit, QCalc, on $3d+1$ qubits that implements:

$$
|x\rangle_d|y\rangle_d|z\rangle_d |0\rangle_d = \begin{cases} |x\rangle_d |y\rangle_d |z\rangle_1 |x+y \text{ mod } 2^d \rangle_d \text{ if } z = 0, |x\rangle_d |y\rangle_d |z\rangle_1 |x \cdot y \text{ mod } 2^d \rangle_d \text{ if } z = 1 \end{cases}
$$


The construction only uses arbitrary 1-qubit gates, CX and Toffoli gates. No classical bit and measurements are used.

The algorithms that we implement are found in the papers https://arxiv.org/pdf/quant-ph/0008033 and https://arxiv.org/pdf/1411.5949.

Our construction uses ancillas in the implementation of our own $C^nP$ gates. As a proof-of-concept, we do not use the in-built Qiskit implementation. This construction is the main bottleneck in the complexity analysis of the circuit, and improving the implementation is left as future work.