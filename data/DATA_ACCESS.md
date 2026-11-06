# Data access and local inputs

The [Baček segmented MATLAB data](https://doi.org/10.26188/24270064.v1) are available from the University of Melbourne's public Figshare release. Cite the associated [Scientific Data publication](https://doi.org/10.1038/s41597-024-03444-4).

The modelling notebooks use a prepared derivative named `bacek_clean_common_angles_metabolic_dataset.h5`. The exact source used to produce the reported results has SHA-256:

`c73ce561e94de52f1dc86128829c43ef536c4cf6b5f4aa9af1ea060409221fa3`

The [MATLAB preparation script](../matlab/build_clean_common_angle_dataset_from_subject_folders.m) expects source folders `All subject data/Sub1/Segmented/` through `All subject data/Sub21/Segmented/` alongside the script and writes its derived files to `Final Processed Data/`. The published source `.mat` files and the prepared `.h5` file are **different artifacts**. An independently verified byte-identical rebuild of the prepared HDF5 has not been demonstrated; compare the checksum before assuming exact input equivalence.

## Local notebook inputs

Place the required files in the notebooks' current working directory, usually `notebooks/`:

- The exact prepared HDF5 for source-dependent modelling and verification.
- `Bacek2023_subject_biological_data.csv` for the biological-input procedures.
- The **original checksum-locked upstream experiment ZIPs**, where required by a notebook. Recompressing the extracted CSVs does not recreate those same archive bytes.
- The fixed E1.3 calibration-trial assignments and E4.2 participant-subset CSV (where specified).
- For EXT-S0, E3.4 and E5.3: the exact reference/extension ZIPs and version-matched protocol amendment and annex documents required by the notebook code.

The two separate E3.4/E5.3 annex files, dated protocol approval and final complete independent N3 verification records are **not included in this public release**. The original E3.4/E5.3 archives recorded the local checks as complete with an independent N3 gate pending. Aggregate result inspection must not be represented as a full independent replay or as completion of that entire gate.

The public repository does not redistribute the HDF5, participant-level biological table or detailed trial-level records. Source-data reuse and further redistribution remain subject to applicable licence and institutional conditions.
