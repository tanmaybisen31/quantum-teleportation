# Quantum Teleportation (Qiskit)

![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg) ![Jupyter Notebook](https://img.shields.io/badge/Jupyter-Notebook-F37626.svg?logo=jupyter&logoColor=white) ![Qiskit](https://img.shields.io/badge/Qiskit-0.31–0.35-6929C4.svg?logo=qiskit&logoColor=white)

A hands-on set of Jupyter notebooks that build up the fundamentals of quantum computing in Qiskit and implement the quantum teleportation protocol.

## Overview

This is a learning project. It works through the basic building blocks of gate-model quantum computing and then uses them to implement quantum teleportation — the protocol that transfers an unknown single-qubit state from one qubit to another using a shared Bell pair and two classical bits.

The teleportation notebook follows the standard textbook construction: prepare a Bell pair, have "Alice" entangle the state qubit with her half of the pair (`CX` then `H`), measure her two qubits, and have "Bob" recover the state by applying `X` and/or `Z` corrections conditioned on those classical measurement results. State transfer is verified visually by comparing the input and output states on the Bloch sphere.

### Notebooks

| Notebook | What it covers |
| --- | --- |
| `building_block.ipynb` | Single-qubit basics: the `X` gate, statevector / unitary / QASM simulators, and reading out a measurement. |
| `HelloWorld.ipynb` | A first 2-qubit circuit — `H` + `CX` to make a Bell state, then measurement, histogram, and Bloch/Q-sphere views. |
| `entanglement.ipynb` | Bell-state entanglement run on both the `qasm_simulator` and a real IBM Quantum backend (`ibmq_belem`). |
| `visualization.ipynb` | Bloch-sphere and Q-sphere visualizations of single-qubit states (`\|0⟩`, `X\|0⟩`, `H\|1⟩`). |
| `teleportation.ipynb` | The full teleportation protocol, step by step, teleporting a random single-qubit statevector using `c_if` conditional corrections. |
| `teleportation2.ipynb` | A compact teleportation circuit on a single 3-qubit register using `CX`/`CZ` corrections instead of classically-conditioned gates. |

## Tech stack

- **Python 3** in **Jupyter Notebook**
- **Qiskit** (0.31–0.35), with Qiskit Aer simulators (`qasm_simulator`, `statevector_simulator`, `unitary_simulator`, `aer_simulator`)
- **Qiskit visualization** (`plot_histogram`, `plot_bloch_multivector`, `plot_state_qsphere`)
- **IBM Quantum** provider for running on real hardware
- NumPy, Matplotlib

## Run

```bash
# create and activate a virtual environment
python -m venv .venv
source .venv/bin/activate      # Windows: .venv\Scripts\activate

# install dependencies
pip install "qiskit==0.35.0" qiskit-aer matplotlib jupyter

# launch
jupyter notebook
```

Open any notebook and run the cells top to bottom. The pure-simulator cells run offline. The cells that call `IBMQ.load_account()` — and especially `entanglement.ipynb`, which submits a job to `ibmq_belem` — require a (free) IBM Quantum account and a saved API token.

## Scope and limitations

- This is an **exploratory / educational** project, not a library or reproducible pipeline. Notebooks are meant to be read and run interactively; there are no automated tests and results are inline plots rather than saved artifacts.
- The code was written against **older Qiskit (0.31–0.35)**. The `IBMQ` provider, `qiskit.ignis`, and several imports used here have since been deprecated or removed in current Qiskit, so newer versions may require changes.
- `ibmq_belem` has since been retired by IBM; the real-hardware cell in `entanglement.ipynb` will need a different, currently-available backend.
- The teleportation construction is based on the approach taught in the IBM Qiskit Textbook.

## License

Released under the [MIT License](LICENSE).
