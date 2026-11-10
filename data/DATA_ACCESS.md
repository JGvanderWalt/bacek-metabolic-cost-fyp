# Data access and local inputs

The [Baček segmented MATLAB data](https://doi.org/10.26188/24270064.v1) are available from the University of Melbourne's public Figshare release. Cite the associated [Scientific Data publication](https://doi.org/10.1038/s41597-024-03444-4).

The modelling notebooks use a prepared derivative named `bacek_clean_common_angles_metabolic_dataset.h5`. The exact source used to produce the reported results has SHA-256:

`c73ce561e94de52f1dc86128829c43ef536c4cf6b5f4aa9af1ea060409221fa3`

The [MATLAB preparation script](../matlab/build_clean_common_angle_dataset_from_subject_folders.m) expects source folders `All subject data/Sub1/Segmented/` through `All subject data/Sub21/Segmented/` alongside the script and writes its derived files to `Final Processed Data/`. The reported analyses use the prepared HDF5 identified by the checksum above. A byte-identical reconstruction from the published segmented MATLAB files has not been verified.

## Local notebook inputs

Place the required files in the notebooks' current working directory, usually `notebooks/`:

- The exact prepared HDF5 for source-dependent modelling and verification.
- `Bacek2023_subject_biological_data.csv` for the biological-input procedures.
- Original experiment ZIP archives with matching SHA-256 hashes, where required by the notebook.
- The fixed E1.3 calibration-trial assignments and E4.2 participant-subset CSV (where specified).
- For EXT-S0, E3.4 and E5.3: the exact reference/extension ZIPs and version-matched protocol amendment and annex documents required by the notebook code.

E3.4 and E5.3 passed local checks and independent N3 numerical verification using retained full-precision prediction and resampling records. The N3 audit did not reconstruct the source HDF5. The N3 verification records, separate protocol annexes and amendment approval record are not included in this repository.

The prepared HDF5, participant-level biological table and detailed trial-level records are retained privately. Access and redistribution are subject to applicable source-data licences and institutional permissions.
