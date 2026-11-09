# MO/ATOM repository audit — 2026-11-09

## Scope

Initial read-only inspection of the repository root on `main`, followed by creation of a separate working branch. This is a partial audit, not a claim that every file or notebook cell has been reviewed.

Repository: `francis44444/Atom`
Baseline: `main`
Working branch: `cleanup/baseline-2026-11-09`

## Confirmed observations

- `README.md` describes `atom_simulation.py`, `mo_tracking.py`, and `climate_feedback.py`, and sketches a GitHub → Colab → IonQ pipeline. The latter two named modules were not found at the repository root during this inspection.
- `atom_simulation.py` reads `agent_config.json`, compares an `emf_frequency` value with the hard-coded target 444.44, and writes `simulation_log.json`. This is a configuration/threshold demonstration, not an atomic or quantum-field simulation. A numerical match to a chosen target is not evidence of physical resonance or stability.
- `agent_config.json` contains `current_project`, `target_variable`, `emf_frequency`, and `status`. It is a small static configuration file, not an agent implementation.
- `unified_control.py` was not found at the repository root.
- `Copy_of_Untitled9.ipynb` is a Colab notebook with a PennyLane installation cell and saved historical outputs. Its opening badge points to a different repository, `francis44444/Unified-Field-Control-`, so its provenance/location should be reconciled before treating it as the canonical Atom notebook.

## Scientific and engineering rules for cleanup

1. Preserve original notebooks, scripts, configuration, and simulator exports; do not delete or silently overwrite them.
2. Separate exploratory ideas, hypotheses, computed results, and externally measured hardware results.
3. Never label a simulator result as an IonQ QPU measurement.
4. Keep secrets out of Git; use Colab Secrets or environment variables for credentials.
5. Pin and test dependencies in a clean environment before changing versions.
6. Keep classical reference calculations, ideal quantum simulation, noisy simulation, and QPU execution as distinct stages.
7. Require explicit human approval before any paid QPU submission or backend change.
8. Record inputs, units, geometry, Hamiltonian, method, software versions, backend, shots, outputs, validation checks, and provenance for each experiment.

## Proposed target layout

```text
.
├── README.md
├── pyproject.toml
├── requirements/
│   ├── base.txt
│   ├── quantum.txt
│   └── dev.txt
├── configs/
│   └── project.example.json
├── src/
│   └── mo_atom/
│       ├── __init__.py
│       ├── provenance.py
│       └── experiments/
│           └── oh_radical/
├── notebooks/
│   └── archive/
├── data/
│   ├── raw/
│   └── processed/
├── results/
├── tests/
└── docs/
```

This layout is a proposal only. Move existing files only after a complete inventory and import/path review.

## Next audit steps

- Inventory every tracked path and notebook cell.
- Identify duplicate code, mixed frameworks, embedded credentials, stale outputs, and environment conflicts.
- Reconcile the Atom and Unified-Field-Control notebook/repository relationship.
- Establish a minimal reproducible environment and smoke tests.
- Refactor incrementally on this branch, with a validation result for each change.
