Aquila Reservation - Completed Task Results
============================================
Generated (UTC): 20260605T143800Z
Completed tasks included: 831

Contents
--------
manifest.json   Structured index of every task (machine-readable).
manifest.csv    Flat table of the same, for quick spreadsheet viewing.
results/        One JSON file per task: the full Braket Analog Hamiltonian
                Simulation result, including every shot's pre_sequence and
                post_sequence, plus task metadata.

File naming
-----------
results/<kind>_<index>__<taskid8>.json
  kind  = train | test   (matches job_ids.json ordering)
  index = position within train_ids / test_ids
  taskid8 = first 8 chars of the Braket quantum-task UUID

Reloading a result in Python
----------------------------
    from braket.tasks import AnalogHamiltonianSimulationQuantumTaskResult as R
    with open("results/train_0__f605a9cc.json") as f:
        result = R.from_string(f.read())
    result.measurements          # list of per-shot measurements
    result.measurements[0].pre_sequence    # atom-detection (1=filled, 0=empty)
    result.measurements[0].post_sequence   # final state per site

Decoding convention
--------------------
Per site, post_sequence value:
    0 -> Rydberg state ("r")
    1 -> ground state  ("g")
<Z_i> = mean over shots of (+1 if ground else -1).
pre_fill_rate in the manifest is the fraction of shots where all atoms were
successfully loaded (a data-quality indicator for the register).

Registers are the 48-atom parallel (6x tiled) layout from the submission
notebook; each 8-site block is one logical problem instance.
