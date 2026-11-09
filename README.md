# Quantum Teleportation and Noise Analysis Using Qiskit

An educational quantum computing project implementing the **Quantum Teleportation Protocol** using Qiskit, with an extended investigation of how quantum noise affects teleportation fidelity.

The project provides two execution approaches:

- **IBM Quantum Hardware:** Execute quantum circuits on real quantum processors through IBM Quantum.
- **Qiskit Aer Simulator:** Simulate quantum circuits locally using a classical computer, without requiring access to IBM Quantum hardware.

The original quantum teleportation implementation is based on IBM's course **"Qiskit in the classroom - computer science"**. This project extends that implementation by introducing quantum noise models, simulation experiments, fidelity analysis, and visualisation using Qiskit Aer.

---

## 1. Project Overview

Quantum teleportation is a fundamental protocol in quantum information science that enables the transfer of an unknown quantum state from one qubit to another using quantum entanglement and classical communication.

It does not physically transport matter or transmit information faster than light. Instead, it transfers the quantum state while the original state is destroyed through measurement.

This project implements the three-qubit quantum teleportation protocol and investigates its behaviour under ideal and noisy conditions.

The project initially follows the teleportation concepts and circuit implementation covered in IBM's *Qiskit in the classroom - computer science* course. It then extends the implementation with a noise-analysis framework to explore how imperfect quantum operations and measurements influence the accuracy of state transfer.

## 2. Project Objectives

- Understand the fundamentals of quantum teleportation.
- Implement the three-qubit teleportation protocol using Qiskit.
- Prepare and teleport different quantum input states.
- Execute circuits using the Qiskit Aer simulator.
- Explore optional execution on IBM Quantum hardware.
- Introduce depolarizing noise and measurement errors.
- Investigate the effect of different noise probabilities on teleportation fidelity.
- Visualise and compare simulation results.
- Understand the differences between ideal simulation, noisy simulation, and real quantum hardware execution.

## 3. Original Work and Project Extension

The project is based on the quantum teleportation implementation introduced in IBM's course:

**Qiskit in the classroom - computer science**

The original course provides the foundation for understanding and implementing the quantum teleportation protocol.

This project extends that foundation with additional experimentation and analysis.

| Component | Source / Contribution |
|---|---|
| Quantum teleportation protocol | Based on IBM's Qiskit classroom course |
| Three-qubit circuit implementation | Adapted from the IBM course implementation |
| Input quantum state preparation | Project implementation |
| Ideal simulation using Qiskit Aer | Project extension |
| Depolarizing noise model | Project extension |
| Readout error model | Project extension |
| Noise probability experiments | Project extension |
| Fidelity estimation and comparison | Project extension |
| Result visualisation and CSV export | Project extension |
| Optional IBM Quantum hardware execution | Additional execution pathway |

**The primary extension of this project is the introduction of a noise-analysis framework to investigate the reliability of quantum teleportation under imperfect quantum operations.**

The IBM course is acknowledged as the educational source for the original teleportation implementation. The additional noise-analysis experiments and associated code are extensions developed for this project.

## 4. Technologies Used

| Technology | Purpose |
|---|---|
| Python | Programming language |
| Qiskit | Quantum circuit construction |
| Qiskit Aer | Ideal and noisy quantum simulation |
| IBM Quantum | Optional real quantum hardware execution |
| Qiskit IBM Runtime | Communication with IBM Quantum backends |
| NumPy | Numerical operations |
| Pandas | Experimental data management |
| Matplotlib | Data visualisation |
| Jupyter Notebook | Interactive development |
| Google Colab | Cloud-based notebook execution |

## 5. Theoretical Background

### 5.1 Quantum State Representation

A general single-qubit pure state is represented as:

$$
|\psi\rangle = \alpha|0\rangle + \beta|1\rangle
$$

where:

$$
|\alpha|^2 + |\beta|^2 = 1
$$

The coefficients $\alpha$ and $\beta$ are complex probability amplitudes.

A qubit can exist in a superposition of the computational basis states $\vert 0\rangle$ and $\vert 1\rangle$.

### 5.2 Quantum Entanglement

Quantum entanglement is a phenomenon in which two or more qubits share correlated quantum states.

The teleportation protocol uses an entangled Bell pair:

$$
|\Phi^+\rangle = \frac{|00\rangle + |11\rangle}{\sqrt{2}}
$$

Alice and Bob share this entangled pair before the teleportation process begins.

### 5.3 Quantum Teleportation Protocol

The protocol uses three qubits:

| Qubit | Role |
|---|---|
| Qubit 0 | Alice's input or secret qubit |
| Qubit 1 | Alice's half of the entangled pair |
| Qubit 2 | Bob's half of the entangled pair |

The teleportation process consists of the following operations:

1. Alice and Bob establish an entangled Bell pair.
2. Alice prepares the input quantum state.
3. Alice performs the Bell-basis operations using CNOT and Hadamard gates.
4. Alice measures her two qubits.
5. The measurement results are communicated classically to Bob.
6. Bob applies conditional correction operations using Pauli-X and Pauli-Z gates.
7. Bob obtains the teleported quantum state.

The original state is destroyed during Alice's measurement, consistent with the no-cloning theorem.

## 6. Quantum States Used in the Experiment

The project investigates three input states:

| State | Description |
|---|---|
| $\vert 0\rangle$ | Computational basis state |
| $\vert 1\rangle$ | Computational basis state |
| $\vert +\rangle$ | Equal superposition state |

The general state is prepared using the Qiskit U gate:

$$
|\psi\rangle = \cos\left(\frac{\theta}{2}\right)|0\rangle + e^{i\phi}\sin\left(\frac{\theta}{2}\right)|1\rangle
$$

These known input states provide a controlled way to test the teleportation circuit.

## 7. Execution Methods

The project supports two execution approaches.

### Method 1: IBM Quantum Hardware

IBM Quantum provides cloud access to real quantum processors.

The teleportation circuit can be transpiled to a compatible IBM backend and executed through Qiskit IBM Runtime.

Real quantum processors introduce physical imperfections, including:

- Single-qubit gate errors
- Two-qubit gate errors
- Qubit decoherence
- Measurement and readout errors
- Connectivity constraints

This execution method provides an opportunity to investigate quantum teleportation on actual quantum hardware.

**Requirements:**

- IBM Quantum account
- Valid IBM Quantum API token
- Access to an available compatible backend
- Qiskit IBM Runtime

The hardware implementation requires support for dynamic circuits and classical feed-forward because Bob's correction operations depend on Alice's measurement outcomes.

### Method 2: Qiskit Aer Simulator

![No IBM account required](https://img.shields.io/badge/No%20IBM%20account-required-success)

The project also uses Qiskit Aer, a high-performance quantum circuit simulator.

This provides an alternative when access to IBM Quantum hardware is unavailable.

Aer allows the teleportation circuit to be executed on a conventional computer, including the CPU runtime available in Google Colab.

The simulator supports:

- Ideal quantum circuit simulation
- Noisy quantum circuit simulation
- Depolarizing noise
- Readout errors
- Measurement statistics
- Fidelity estimation

The Aer implementation makes the project independently executable without IBM Quantum credentials or access to a physical quantum processor.

## 8. Quantum Noise Analysis

An important extension of the original teleportation implementation is the introduction of quantum noise models.

Real quantum computers are not perfectly isolated systems. Environmental interactions and imperfect quantum operations can affect the state of a qubit.

This project investigates two types of noise.

### 8.1 Depolarizing Noise

Depolarizing noise represents a quantum channel that introduces errors by mixing the original quantum state with the maximally mixed state.

It can be represented as:

$$
\mathcal{E}(\rho) = (1-p)\rho + p\frac{I}{2^n}
$$

where:

- $\rho$ is the original density matrix.
- $I$ is the identity matrix.
- $p$ is the depolarizing noise parameter.
- $n$ is the number of qubits.

In this project, depolarizing errors are applied to:

- Single-qubit U gates.
- Two-qubit CNOT gates.

### 8.2 Readout Error

Readout errors occur when a measurement returns an incorrect classical result.

For example:

- A qubit in state $\vert 0\rangle$ may be measured as `1`.
- A qubit in state $\vert 1\rangle$ may be measured as `0`.

The project uses a symmetric readout error model:

$$
P(0 \rightarrow 1) = p, \qquad P(1 \rightarrow 0) = p
$$

This allows the effect of measurement imperfections on teleportation verification to be investigated.

### 8.3 Noise Probability Experiments

The simulation evaluates multiple noise probabilities:

```python
noise_levels = [0.0, 0.001, 0.005, 0.01, 0.02, 0.05]
```

For each noise level, the teleportation circuit is executed for all three input states.

The resulting fidelity values are recorded and compared.

The same parameter $p$ is used as a convenient control for both gate and readout noise. It should not be interpreted as a calibrated hardware error rate.

## 9. Fidelity Analysis

Fidelity measures how closely a received quantum state matches its intended target state.

For pure states:

$$
F = \left|\langle\psi_{\text{target}}|\psi_{\text{received}}\rangle\right|^2
$$

In this project, Bob's state is verified by applying the inverse of Alice's known state-preparation operation before measurement.

If Bob has received the correct state, the verification measurement should ideally return `0`.

The estimated verification fidelity is calculated as:

$$
F_{\text{estimated}} = \frac{\text{Successful verification outcomes}}{\text{Total measurement shots}}
$$

This is a measurement-based verification estimate for the known input states used in the experiment. It is not full quantum state tomography.

The results are used to investigate how increasing noise affects the probability of successfully verifying the teleported state.

## 10. Experimental Workflow

```text
          Input Quantum State
                   |
                   v
       Quantum Teleportation Circuit
                   |
                   v
          Bell Pair Generation
                   |
                   v
       Alice's Bell-Basis Operations
                   |
                   v
           Classical Measurement
                   |
                   v
        Bob's Conditional Corrections
                   |
                   v
          State Verification
                   |
                   v
          Ideal Aer Simulation
                   |
                   v
         Introduce Noise Models
                   |
                   v
          Noisy Aer Simulation
                   |
                   v
           Fidelity Estimation
                   |
                   v
         Noise Analysis and Plots
                   |
                   v
            Export Results
```

IBM Quantum hardware execution is an optional additional pathway.

## 11. Results and Visualisation

The notebook generates experimental results for different input states and noise probabilities.

The visualisations include:

1. **Fidelity by input state vs noise probability** – compares how the three input states respond to different noise levels.
2. **Mean fidelity vs noise probability** – shows the average verification fidelity across all three input states.

The notebook also exports:

- Ideal simulation results.
- Noisy simulation results.
- Fidelity plots.
- CSV files containing experimental measurements.

The expected general behaviour is that increasing noise will reduce teleportation verification fidelity. Actual numerical values should be obtained by executing the notebook rather than assumed in advance.

## 12. Installation and Setup

### Requirements

- Python 3.10 or a compatible Python environment
- Google Colab or Jupyter Notebook
- Internet access for initial package installation

### Install Dependencies

```bash
pip install qiskit qiskit-aer qiskit-ibm-runtime numpy pandas matplotlib pylatexenc
```

### Run Using Google Colab

1. Download or clone this repository.
2. Open [Google Colab](https://colab.research.google.com/).
3. Select **File → Upload notebook**.
4. Upload `Quantum_Teleportation_Noise_Analysis_Colab.ipynb`.
5. Select a CPU runtime.
6. Execute the notebook cells sequentially.

The Aer simulator and noise-analysis sections do not require IBM Quantum credentials.

### Optional IBM Quantum Authentication

For IBM hardware execution:

1. Create an account at [IBM Quantum](https://quantum.ibm.com/).
2. Generate an IBM Quantum API token.
3. Open the Colab Secrets panel.
4. Create a secret named `IBM_QUANTUM_TOKEN`.
5. Store your API token as the secret value.
6. Enable notebook access to that secret.
7. Set `RUN_IBM = True` in the optional hardware execution cell.

> **Warning:** Never hardcode your API token into the notebook or commit it to GitHub.

Hardware execution depends on account access, backend availability, and support for dynamic circuits.

## 13. Repository Structure

```text
quantum-teleportation-noise-analysis/
│
├── Quantum_Teleportation_Noise_Analysis_Colab.ipynb
│
├── results/
│   ├── fidelity_by_state_vs_noise.png
│   ├── mean_fidelity_vs_noise.png
│   ├── noise_analysis_results.csv
│   └── ideal_simulation_results.csv
│
├── README.md
├── requirements.txt
└── .gitignore
```

The `results/` directory is populated when the notebook is executed.

## 14. Limitations

- The noise models are simplified mathematical models and do not represent a fully calibrated IBM quantum processor.
- The same noise parameter is used to control multiple error channels for experimental convenience.
- The fidelity calculation is based on verification of known input states, not full quantum state tomography.
- Real hardware results may differ from simulated results due to device calibration, coherence, connectivity, and sampling effects.
- IBM Quantum hardware execution is optional and depends on backend availability and dynamic-circuit support.

## 15. Future Scope

Potential improvements include:

- Comparing ideal simulation, noisy simulation, and real IBM hardware results.
- Using hardware-derived noise properties to construct more realistic Aer simulations.
- Investigating additional noise channels, including amplitude damping and phase damping.
- Studying the effect of different shot counts on fidelity estimation.
- Implementing quantum state tomography.
- Comparing teleportation performance across different quantum backends.

## 16. References and Acknowledgements

**Original learning resource and teleportation implementation:**

IBM — *Qiskit in the classroom - computer science*.

The quantum teleportation implementation in this project is based on the material covered in this IBM course. The noise modelling, Aer-based noise experiments, fidelity analysis, result visualisation, and associated extensions were added as part of this project.

Additional references:

1. Bennett et al. (1993), *Teleporting an Unknown Quantum State via Dual Classical and Einstein-Podolsky-Rosen Channels*, Physical Review Letters. https://doi.org/10.1103/PhysRevLett.70.1895
2. Qiskit Documentation: https://docs.quantum.ibm.com/
3. Qiskit Aer Documentation: https://qiskit.github.io/qiskit-aer/
4. Qiskit IBM Runtime Documentation: https://quantum.cloud.ibm.com/docs/

---

## Author

**Anagha Vinod**

MSc Physics | Quantum Computing | Quantum Information

GitHub: https://github.com/anaghavinod2000

## License

This project is intended for educational and research purposes. The original teleportation implementation is based on the IBM course acknowledged above. The additional project extensions are provided for learning, experimentation, and further development.
