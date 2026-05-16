# Quantum Drone Routing

This repository contains the implementation and analysis of a hybrid quantum-classical framework designed to solve the Vehicle Routing Problem with spatio-temporal collision constraints. The project specifically compares the performance of the standard Quantum Approximate Optimization Algorithm (QAOA) against a specialized QAOA Ansatz utilizing the XY-mixer to navigate a $21 \times 21$ discrete grid.

## Project Overview

The goal is to assign optimal routes to a fleet of drones while ensuring no two vehicles occupy the same grid coordinates within a critical time threshold $\Delta$.

## Features
- Problem Stance: Two drones, Three routes for each on a $21 \times 21$ discrete 2D lattice
- Framework: A hybrid pipeline that maps physical routing constraints into a QUBO (Quadratic Unconstrained Binary Optimization) formulation.
- Quantum Platform: Developed using the Ket quantum programming language and simulation environment.
- Noise Analysis: Includes comparative studies between ideal (noiseless) simulations and noisy scenarios to evaluate algorithmic robustness.

## Contribuitions
### Hybrid Confliting Mapping
Unlike traditional approaches that attempt to solve pathfinding directly on the quantum processor, this project introduces a Hybrid Spatio-Temporal Collision Model. Instead of encoding the entire grid physics into the Hamiltonian, we perform a classical search to identify spatio-temporal conflicts between candidate route pairs. These identified conflicts are mapped into a specific penalty term in the QUBO formulation. By shifting the collision detection to the classical pre-processing stage, we drastically reduce the number of required gates and qubits, making it feasible for Near-term Intermediate-Scale Quantum (NISQ) devices.

### Comparative analysis between standard QAOA and QAOA Ansatz
The QAOA Ansatz utilizes the XY-mixer, which structurally enforces the "one-hot" constraint (one route per vehicle). By restricting the quantum evolution to the feasible subspace, we achieve a massive reduction in search space complexity:
- Standard QAOA ($X$-mixer): Explores $2^n = 2^6 = 64$ states.
- QAOA Ansatz ($XY$-mixer): Explores only $|\mathcal{R}|^{|V|} = 3^2 = 9$ states.

This represents an ~86% reduction in search space for the 2-drone/3-route instance, significantly improving the algorithm's accuracy.

## Results Summary
Our findings indicate that while the standard QAOA struggles with constraint satisfaction in noisy environments, the QAOA Ansatz maintains a higher success probability by preventing the system from collapsing into invalid (non-one-hot) states.

## Repository Structure
`drone.ipynb`: The main Jupyter Notebook containing the problem definition, Hamiltonian construction, and simulation results.

`requirements.txt`: Necessary Python libraries and Ket dependencies.

## Authors
- Kalleb C. Santos
- Maria Eduarda W. M. Vianna
- Mateus K. de Oliveira
- Evandro Chagas Ribeiro da Rosa
- Alison R. Panisson
- Luiz F. Bittencourt
- Roberto Rodrigues-Filho
