# Polarisation curves at ageing checkpoints for 57 proton exchange membrane fuel cells from 4 laboratories

Version 1.4.0. This repository holds the data and metadata of the release, file by file: every file is byte-identical to the release, and its SHA-256 is listed in `MIRROR_MANIFEST.json`. The archival release, with the code that builds and verifies it, is deposited on Zenodo; its DOI is added here when it is published.

Tables: data.csv (the polarisation checkpoints of the four extension sources), data/cells.csv (one row per cell, with the Fraunhofer cathode and stressor parameters per cell and each source's DOI), data/sources.csv (one row per input: identifier, custodian, title, DOI, landing page, licence), data/zsw_setpoint_holds.csv (the ZSW set-point holds: last-30-s means per set point and direction, with the JRC 7.1 station columns), data/fraunhofer_characterisation_pointers.csv (where each EIS, CV, LSV and limiting-current file of the counted Fraunhofer cells sits in the custodian's archives; those files are not carried), data/uncounted_cell_rows.csv (the one-checkpoint PoliMi cell, not counted), split_by_cell.csv and split_by_stack.csv; every other file under data/ is a column dictionary listed in the release record with role schema. 18436 rows of polarisation checkpoints, 57 cells with at least two ageing checkpoints (Fraunhofer ISE / TRI 37, RWTH 8, PoliMi 2, ZSW 10). Measurand: cell voltage (V) against current density (A/cm2) at a stated ageing checkpoint, with the operating conditions each custodian recorded carried per row (see conditions_source). The ageing axis is NOT harmonised: hours for PoliMi and ZSW; accelerated-stress cycles for Fraunhofer and RWTH (two different kinds of cycle). ZSW sweeps are binned to 0.02 A/cm2 by median voltage; point tables are kept as published; RWTH mV converted to V. Every row, channel, block or cell the build excluded is in exclusions.json with its rule and count. Checkpoints: every ZSW nominal polarisation file of the deposit is read (11 files). The 2 files named _afterAirAirStart (labels 1500 and 2300 h) hold the curve recorded after a passive air/air start-up, which the custodian added to measure reversible losses; their rows carry checkpoint_kind recovery_event, an empty checkpoint_index and a recovery_event_index, and they are not counted as ageing checkpoints. Every other row is checkpoint_kind ageing. The ZSW cells have 9 ordinary ageing checkpoints each, the last at the 2300 h label. LICENCE: Creative Commons Attribution 4.0 International (CC-BY-4.0). every byte in this variant comes from the four CC BY 4.0 sources; the FCLAB base (CC BY-NC-SA 3.0) is NOT included and is fetched by the user with the recipe in README.md, so no NonCommercial or ShareAlike condition attaches Attribution to every upstream creator, with identifiers, licence URIs and requested citations, is in NOTICE.txt. Licence: CC-BY-4.0 for the whole release (LICENSE.txt); attribution to every source is in NOTICE.txt.

## Creator

Yueqiang Xu, University of Oulu. ORCID: https://orcid.org/0000-0002-3528-423X

## How to cite

Use `CITATION.cff` (GitHub shows it under "Cite this repository"), and cite the source data this release is derived from:

- Schneider, P., Scherzer, A.-C., Ney, L., Kwon, H.-K., Storey, B. D., Gerteisen, D., &amp; Zamel, N. (2024). <i><b>In-Situ Characterization of Cathode Catalyst Degradation in PEM Fuel Cells</b></i> [Data set]. figshare. https://doi.org/10.6084/M9.FIGSHARE.25450177
- Thiele, P., Yang, Y., Dirkes, S., Wick, M., &amp; Pischinger, S. (2024). <i>Dataset to: Realistic accelerated stress tests for PEM fuel cells: Test procedure development based on standardized automotive driving cycles</i> (Version v1.0) [Data set]. Zenodo. https://doi.org/10.5281/ZENODO.13166135
- Elena, C., Andrea, B., Andrea, B., Guetaz Laure, &amp; Andrea, C. (2022). <i>Dataset of "PEMFC performance decay during real-world automotive operation: evincing degradation mechanisms and heterogeneity of ageing"</i> [Data set]. Zenodo. https://doi.org/10.5281/ZENODO.7054555
- Fensterle, E., Hunger, J., Rabsahl, F., Wilhelm, F., Kolle Christensen, C., Benson, A., Al-Khamissi, R., Trégaro, M., Escribano, S., Scholta, J., &amp; Hölzle, M. (2026). <i>Underlying data of the paper "Spatially Resolved Electrochemical Characterization of a PEM Fuel Cell Stack During Durability Testing"</i> [Data set]. Zentrum für Sonnenenergie- und Wasserstoff-Forschung Baden-Württemberg (ZSW). https://doi.org/10.5281/ZENODO.20715542

## Licence

cc-by-4.0. The licence text and any attribution notice required by the sources are in the licence and notice files of this repository; they travel with every copy.

## Files in the repository

| path | bytes |
|---|---|
| column_dictionary.json | 9,421 |
| croissant.json | 71,019 |
| data/cells.csv | 17,378 |
| data/cells_column_dictionary.json | 5,044 |
| data/column_dictionary.json | 9,421 |
| data/fraunhofer_characterisation_pointers.csv | 583,615 |
| data/fraunhofer_characterisation_pointers_column_dictionary.json | 2,198 |
| data/sources.csv | 1,679 |
| data/sources_column_dictionary.json | 1,782 |
| data/split_by_cell_column_dictionary.json | 369 |
| data/split_by_stack_column_dictionary.json | 598 |
| data/uncounted_cell_rows.csv | 6,648 |
| data/uncounted_cell_rows_column_dictionary.json | 9,400 |
| data/zsw_setpoint_holds.csv | 928,391 |
| data/zsw_setpoint_holds_column_dictionary.json | 8,727 |
| data.csv | 11,891,316 |
| exclusions.json | 8,492 |
| LICENSE.txt | 1,447 |
| NOTICE.txt | 6,009 |
| proof/FACTS.json | 6,734 |
| proof/MANIFEST.json | 4,708 |
| docs/RELEASE_README.md | 8,746 |
| release_meta.json | 18,877 |
| split_by_cell.csv | 1,405 |
| split_by_stack.csv | 2,338 |

## Files attached to the GitHub release (larger than 50 MB)

| path | asset name | bytes |
|---|---|---|
| (none) | | |

## Not in this repository

10 file(s) of the release are not here: code, build logs, change history and build provenance records. `MIRROR_MANIFEST.json` lists each one; all are in the archival release.
