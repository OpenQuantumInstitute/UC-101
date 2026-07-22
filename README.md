# UC-101

**OQI UC-101: Accelerating Novel Antimicrobial Discovery** — an [Open Quantum Institute](https://oqi.ch) use case applying quantum reservoir computing (QRC) to antimicrobial resistance (AMR) drug discovery.

This repository hosts the data for first hardware execution of the QRC pipeline, run on an 8-qubit neutral-atom QPU (Amazon Braket's Aquila device) arranged in a 4×2 grid with 6 parallelized register blocks (~90 effective shots per molecule). A classical reservoir computing (CRC) baseline using echo state networks was built alongside it to isolate genuinely quantum contributions from generic nonlinear feature expansion. The primary prediction target is the dipole P kurtosis ($D_{p,\text{kurt}}$), a molecular property relevant to antibiotic membrane permeability.

Hardware results showed QRC features alone did not significantly improve predictions at the tested shot count, though combined QRC+CRC features gave modest gains for $D_{p,\text{mean}}$. Hardware throughput was well below expectations (139 molecules processed vs. ~900 expected), inflating per-molecule cost, but the approach remains scientifically plausible with an estimated 30–fold energy reduction over classical GPU-based simulation.

This repository contains the data generation notebooks behind that report.

## Notebook to report mapping

| Report item | Notebook |
| --- | --- |
| Figure 1: The advantage of quantum reservoir computing for a variety of the dipole properties vs shot count. The property that we are targeting is Dp kurtosis which quickly gains an advantage. | [`notebooks/noiseless_shots_comparison.ipynb`](notebooks/noiseless_shots_comparison.ipynb) |
| Table 1: R2 Comparing QRC and linear feature embeddings for 100 shots of noisy initialization and atom placement. You can see that the targetted Dp,kurt still retains an advantage of 0.145. This may be due to luck but indicates that using 100 shots may have been enough for separation on quantum hardware. | [`notebooks/noisy_analysis_12_qubits.ipynb`](notebooks/noisy_analysis_12_qubits.ipynb) |
| Hardware analysis: Experimental results for various combinations of classical and quantum reservoirs. A positive ∆R2 indicates that the reservoir augmented model beat the Linear model. The experimentally derived quantum features do not significantly change the results in any of the cases. L represents only linear regression, C adds CRC features, Q adds QRC features. | [`notebooks/quantum_and_classical_reservoir_computing.ipynb`](notebooks/quantum_and_classical_reservoir_computing.ipynb) |
| Process hardware data | [`notebooks/process_data.ipynb`](notebooks/process_data.ipynb) |
