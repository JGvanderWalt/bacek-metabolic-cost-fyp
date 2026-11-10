# Walking metabolic cost prediction from gait kinematics

Python and MATLAB code for a machine-learning feasibility investigation using the Baček walking dataset. The study estimates **mean steady-state net metabolic power (W/kg)** from optical gait kinematics and tests whether measured gait improves prediction beyond prescribed walking conditions.

The primary evaluation uses **284 unrestricted walking trials from 21 participants**, with participant-disjoint model evaluation. A separate experiment examines calibration for known individuals using designated labelled trials.

## Principal results

| Prediction procedure | Held-out root mean squared error (RMSE; W/kg) |
| --- | ---: |
| Training-mean reference (B0) | 0.9685 |
| Development-selected gait (G) | 0.6026 |
| Prescribed speed and relative cadence (C) | 0.5588 |
| Prescribed conditions plus gait (C+G) | 0.6425 |

The gait-only procedure achieved lower error than the training-mean reference, while the tested combined procedure had higher error than prescribed conditions alone. The participant-held-out folds were inspected during exploratory development; these estimates are **exploratory-informed**, and external-cohort performance remains untested.

## Files

- [`notebooks/`](notebooks/) — experimental and verification notebook source code (17 files).
- [`matlab/`](matlab/) — script for preparing the common-angle HDF5 input.
- [`results/`](results/) — saved aggregate error measures, comparisons, and uncertainty summaries.
- [`data/DATA_ACCESS.md`](data/DATA_ACCESS.md) — source data access and local-input requirements.

The repository provides code and aggregate results. The prepared HDF5, biological input table, fixed assignment manifests and detailed execution records are retained separately. Full reproduction requires these inputs; see the [data-access guide](data/DATA_ACCESS.md).

## Script-to-output guide

| Scripts | Purpose | Principal output |
| --- | --- | --- |
| [MATLAB dataset builder](matlab/build_clean_common_angle_dataset_from_subject_folders.m) | Prepare the nine-angle, trial-linked analysis input from segmented Baček files. | `bacek_clean_common_angles_metabolic_dataset.h5` (local only). |
| [02](notebooks/02_Bacek_Numerical_Integrity_Preflight.ipynb), [03](notebooks/03_Bacek_Gait_Feature_Pipeline_Verification.ipynb) | Check numerical source integrity and synthetic feature/pipeline behaviour. | Source-integrity and verification records (retained privately). |
| [04](notebooks/04_Bacek_Foundational_Predictive_Models.ipynb), [11](notebooks/11_Bacek_Known_Person_Calibration.ipynb) | Evaluate population references and gait models; separately evaluate known-person calibration. | [Foundational metrics](results/E1_2_reference_and_gait_metrics.csv), [calibration metrics](results/E1_3_known_person_metrics.csv). |
| [05](notebooks/05_Bacek_Incremental_Gait_Information.ipynb), [06](notebooks/06_Bacek_Biological_Information_Comparison.ipynb) | Compare the added predictive value of gait alongside prescribed conditions and age/height. | [Condition–gait comparison](results/E2_1_incremental_gait_metrics.csv), [biological-input comparison](results/E2_2_biological_input_metrics.csv). |
| [07](notebooks/07_Bacek_Anatomical_Gait_Information.ipynb), [08](notebooks/08_Bacek_Descriptor_Family_Comparison.ipynb), [12](notebooks/12_Bacek_285_Trial_Eligibility_Sensitivity.ipynb) | Compare anatomical groups and descriptor families; check 285-trial eligibility sensitivity. | [Anatomical groups](results/E3_1_anatomical_group_metrics.csv), [descriptor families](results/E3_3_descriptor_family_metrics.csv), [eligibility sensitivity](results/E3_2_eligibility_sensitivity_metrics.csv). |
| [09](notebooks/09_Bacek_Ridge_vs_RBF_SVR_Comparison.ipynb), [10](notebooks/10_Bacek_Regularisation_Training_Participant_Sufficiency.ipynb) | Compare Ridge and radial-basis-function support vector regression (RBF-SVR); examine regularisation and training-participant budgets. | [Model comparison](results/E4_1_ridge_svr_metrics.csv), [training-budget metrics](results/E4_2_training_budget_metrics.csv). |
| [13](notebooks/13_Bacek_Participant_Condition_Error_Diagnostics.ipynb), [14](notebooks/14_Bacek_Clustered_Uncertainty_Influence_Selection_Stability.ipynb), [15](notebooks/15_Bacek_Computational_Repeatability_Requirements_Audit.ipynb) | Examine prediction error, clustered uncertainty, influence, selection stability and computational verification. | [Error diagnostics](results/E5_1_overall_diagnostics_metrics.csv), [bootstrap intervals](results/E5_2_paired_bootstrap_intervals.csv), [balanced metrics](results/E5_2_participant_balanced_metrics.csv), [independent metric recalculation](results/independent_primary_metric_recalculation.csv). |
| [17 (EXT-S0)](notebooks/17_EXT_S0_Shared_Source_Feature_Preflight.ipynb), [E3.4](notebooks/E3_4_Between_Cycle_Variability_Local.ipynb), [E5.3](notebooks/E5_3_Retained_Cycle_Budget_Local.ipynb) | Verify shared feature inputs; assess between-cycle dispersion and retained-cycle observation budgets. | [Variability metrics](results/E3_4_cycle_variability_metrics.csv) and [intervals](results/E3_4_cycle_variability_intervals.csv); [cycle-budget metrics](results/E5_3_cycle_budget_metrics.csv) and [intervals](results/E5_3_cycle_budget_intervals.csv). |

The linked CSVs provide aggregate results; the notebooks also generate detailed prediction, selection, provenance and verification records retained privately. E3.4 and E5.3 passed local checks and independent N3 numerical verification (322/322 checks) using retained full-precision records.

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

Run notebooks from `notebooks/` as the working directory. The [data-access guide](data/DATA_ACCESS.md) specifies the prepared HDF5, fixed manifests and checksum-matched original ZIP archives required for execution.

## Source

Baček, T. et al. *A biomechanics and energetics dataset of neurotypical adults walking with and without kinematic constraints*. *Scientific Data*, **11**, 646 (2024). [Article](https://doi.org/10.1038/s41597-024-03444-4) · [Segmented MATLAB dataset](https://doi.org/10.26188/24270064.v1).
