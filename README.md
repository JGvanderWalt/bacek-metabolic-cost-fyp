# Walking metabolic cost prediction from gait kinematics

Python and MATLAB code for a machine-learning feasibility investigation using the Baček walking dataset. The study estimates **mean steady-state net metabolic power (W/kg)** from optical gait kinematics and tests whether measured gait improves prediction beyond prescribed walking conditions.

The primary evaluation uses **284 unrestricted walking trials from 21 participants**, with participant-disjoint model evaluation. A separate experiment examines calibration for known individuals using designated labelled trials.

## Principal results

| Prediction procedure | Held-out RMSE (W/kg) |
| --- | ---: |
| Training-mean reference (B0) | 0.9685 |
| Development-selected gait (G) | 0.6026 |
| Prescribed speed and relative cadence (C) | 0.5588 |
| Prescribed conditions plus gait (C+G) | 0.6425 |

The gait-only procedure improves on the constant reference, but the tested combined procedure does not improve upon prescribed walking conditions alone. The outer folds had been inspected during exploratory work, so these results are **internally held-out and exploratory-informed**, not independent external validation.

## Files

- [`notebooks/`](notebooks/) — experimental and verification notebook source code (17 files).
- [`matlab/`](matlab/) — script for preparing the common-angle HDF5 input.
- [`results/`](results/) — saved aggregate error measures, comparisons, and uncertainty summaries.
- [`data/DATA_ACCESS.md`](data/DATA_ACCESS.md) — source data access and local-input requirements.

The public release contains code and **aggregate results only**. It does not include the prepared HDF5, biological participant table, individual-trial predictions, exact experiment execution archives, or fixed assignment manifests. These inputs are needed for a complete rerun or independent record-level verification.

## Python environment

Use **Python 3.11.1**. From the repository root:

```bash
python -m venv .venv
```

Activate the environment using `.venv\Scripts\activate` in Windows Command Prompt, or `source .venv/bin/activate` on macOS/Linux. Then install the requirements and launch Jupyter:

```bash
python -m pip install -r requirements.txt
python -m notebook
```

Run notebooks from `notebooks/` as the working directory. Place the required local inputs there, as specified by each notebook and the [data-access guide](data/DATA_ACCESS.md). Some notebooks require original hash-matched ZIPs; the aggregate CSVs in this repository cannot replace those source archives. The original results were generated in a documented environment; a fresh public-source rerun has not been independently established.

## Source

Baček, T. et al. *A biomechanics and energetics dataset of neurotypical adults walking with and without kinematic constraints*. *Scientific Data*, **11**, 646 (2024). [Article](https://doi.org/10.1038/s41597-024-03444-4) · [Segmented MATLAB dataset](https://doi.org/10.26188/24270064.v1).
