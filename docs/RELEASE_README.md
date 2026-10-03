PEM fuel cell durability collection: polarisation curves at ageing checkpoints - extension only, CC BY variant (the deposited release)
======================================================================

Tables: data.csv (the polarisation checkpoints of the four extension sources), data/cells.csv (one row per cell, with the Fraunhofer cathode and stressor parameters per cell and each source's DOI), data/sources.csv (one row per input: identifier, custodian, title, DOI, landing page, licence), data/zsw_setpoint_holds.csv (the ZSW set-point holds: last-30-s means per set point and direction, with the JRC 7.1 station columns), data/fraunhofer_characterisation_pointers.csv (where each EIS, CV, LSV and limiting-current file of the counted Fraunhofer cells sits in the custodian's archives; those files are not carried), data/uncounted_cell_rows.csv (the one-checkpoint PoliMi cell, not counted), split_by_cell.csv and split_by_stack.csv; every other file under data/ is a column dictionary listed in the release record with role schema.

18436 rows of polarisation checkpoints, 57 cells with at least two ageing checkpoints (Fraunhofer ISE / TRI 37, RWTH 8, PoliMi 2, ZSW 10).
Measurand: cell voltage (V) against current density (A/cm2) at a stated ageing checkpoint, with the operating
conditions each custodian recorded carried per row (see conditions_source). The ageing axis is NOT harmonised:
hours for PoliMi and ZSW; accelerated-stress cycles for Fraunhofer and RWTH (two different kinds of cycle). ZSW sweeps are
binned to 0.02 A/cm2 by median voltage; point tables are kept as published; RWTH mV converted to V.
Every row, channel, block or cell the build excluded is in exclusions.json with its rule and count.

Checkpoints: every ZSW nominal polarisation file of the deposit is read (11 files). The 2 files named _afterAirAirStart (labels 1500 and 2300 h) hold the curve recorded after a passive air/air start-up, which the custodian added to measure reversible losses; their rows carry checkpoint_kind recovery_event, an empty checkpoint_index and a recovery_event_index, and they are not counted as ageing checkpoints. Every other row is checkpoint_kind ageing. The ZSW cells have 9 ordinary ageing checkpoints each, the last at the 2300 h label.

LICENCE: Creative Commons Attribution 4.0 International (CC-BY-4.0). every byte in this variant comes from the four CC BY 4.0 sources; the FCLAB base (CC BY-NC-SA 3.0) is NOT included and is fetched by the user with the recipe in README.md, so no NonCommercial or ShareAlike condition attaches

Attribution to every upstream creator, with identifiers, licence URIs and requested citations, is in NOTICE.txt.

Rebuild: python rebuild/rebuild_dpo04.py --raw-dir <folder>   (this release's own script, no lab code: it fetches the four sources by DOI, rebuilds every table and compares it with this release; see How to verify, check 2)

## What this collection is for

It suits comparison of polarisation-curve degradation across laboratories, accelerated-stress-test protocols and catalyst-layer materials: one row schema, the recorded operating conditions per row, and the per-cell design and stressor parameters of the Fraunhofer cells. It is not a prognostics dataset: the polarisation table has 2 to 9 ordinary ageing checkpoints per cell, no common end-of-life criterion and no remaining-useful-life target. For remaining-useful-life and voltage-trajectory models use the custodians' time series directly: the FCLAB IEEE PHM 2014 ageing series (doi:10.25666/DATAUBFC-2021-07-19), the ZSW heavy-duty load-cycle record (Loadcycle_data.zip in doi:10.5281/zenodo.20715542) and the PoliMi operando voltage files (Operando voltage_CCMA/B/C.csv in doi:10.5281/zenodo.7054555).

The Fraunhofer cells are also described by the custodian's own Data Descriptor (doi:10.1038/s41597-024-03662-w). Over that deposit this collection adds the curves of three other custodians in the same schema, the conditions per row, the cell-level de-duplication, train and test splits that keep cells and stacks on one side, and a rebuild script. It drops the Fraunhofer impedance spectra, cyclic voltammetry, linear sweep voltammetry and limiting-current data (CC BY 4.0, inside the custodian's cell archives); data/fraunhofer_characterisation_pointers.csv lists each such file of each counted cell with its archive, path, size and CRC-32.

## Recipe to rebuild the union (base plus this deposit) on your own machine

The base is NOT in this deposit. It is the IEEE PHM 2014 Data Challenge archive of FCLAB, doi:10.25666/DATAUBFC-2021-07-19, creator Fabien Harel, licence CC-BY-NC-SA-3.0 <https://creativecommons.org/licenses/by-nc-sa/3.0/>, served by the custodian at https://search-data.ubfc.fr/FR-18008901306731-2021-07-19_IEEE-PHM-Data-Challenge-2014.html.

1. Fetch the archive (47725228 bytes, expected sha256 de09222c60674b9625d2eb45b0bdec4b890e9c1d98645cf4501ca8d3bc29d992):

       curl -L 'https://search-data.ubfc.fr/dl_data.php?file=97' -o RAW/fclab/FC1_FC2_Excel.zip
       sha256sum RAW/fclab/FC1_FC2_Excel.zip

2. The four extension sources' files go beside it under the custodians' own file names (RAW/fraunhofer_ise_tri/Cell_XX.zip and data_overview.xlsx, RAW/rwth_realageing/DataSet.zip, RAW/polimi/Reference polarization curve_ageing.csv, RAW/zsw_hyfab/Polcurve_Nominal_RHFC_*.csv, all 11 nominal ZSW files); every file's sha256 is in rebuild/expected_raw_sha256.json, and step 3 downloads any file that is missing.

3. Run this release's own rebuild script in union mode:

       python rebuild/rebuild_dpo04.py --variant union --raw-dir RAW --out UNION

rebuild/rebuild_dpo04.py is self-contained (Python 3.10+, pandas, openpyxl; it imports no lab code). It checks every raw file against rebuild/expected_raw_sha256.json and writes the union tables to UNION. This CC BY release holds no base rows, so in union mode the script does not compare its tables with it; it reports the build and exits 0.
The union you build is CC BY-NC-SA 4.0 and its conditions are yours to honour. Requested citation for the base: Fabien Harel (2021): IEEE PHM Data Challenge 2014 . dataUBFC. doi:10.25666/DATAUBFC-2021-07-19

## Splits

split_by_cell.csv holds out about a quarter of the cells of EACH source (seeded shuffle within source; a source with two cells holds out none, because 0.25 x 2 rounds to 0): test cells by source {'fraunhofer_ise_tri': 9, 'rwth_realageing': 2, 'zsw_hyfab': 2} of {'fraunhofer_ise_tri': 37, 'zsw_hyfab': 10, 'rwth_realageing': 8, 'polimi': 2}. Cells of one stack can sit on both sides of this split, so a model can learn a stack's ageing trajectory from sibling cells. split_by_stack.csv assigns each cell to a group, its stack where the source names one and the cell itself otherwise, and holds out whole groups: 11 groups are held out, of which 1 is a multi-cell stack (Stack2) and the rest single cells; ZSW has one stack, which cannot be held out and stays in train. Both splits are verified disjoint and their leakage runs are on the record.

## How to verify

Two checks, both runnable without any lab code (Python 3.10+, pandas; the rebuild also needs openpyxl).

1. Integrity and every stated number: `python verify_release.py` checks each file against proof/MANIFEST.json
   (sha256 and size), refuses unlisted files, reruns proof/recompute_facts.py (reads only this folder) and compares
   every recomputed number and licence-chain string with proof/FACTS.json, which the builder wrote from its own
   pipeline records, not from that script. Exit code 0 means all agree.
2. Rebuild from the custodians' own deposits: `python rebuild/rebuild_dpo04.py --raw-dir <folder>` resolves each
   DOI at doi.org, downloads the files the build reads from the repository (figshare or Zenodo API), checks the
   repository md5 and the sha256 in rebuild/expected_raw_sha256.json, rebuilds the tables with the build logic
   vendored import-free, and compares every rebuilt table with this release byte by byte and row by row.

Builder's run of release 1.4.0 (2026-09-28T15:16:55+00:00, summary in rebuild/REBUILD_RESULT.json): 56 raw files, sha256 as expected: yes;
- data.csv: byte-identical yes; 18436 rows rebuilt, 0 only in the rebuild, 0 only in the release
- data/cells.csv: byte-identical yes; 57 rows rebuilt, 0 only in the rebuild, 0 only in the release
- data/fraunhofer_characterisation_pointers.csv: byte-identical yes; 5327 rows rebuilt, 0 only in the rebuild, 0 only in the release
- data/uncounted_cell_rows.csv: byte-identical yes; 16 rows rebuilt, 0 only in the rebuild, 0 only in the release
- data/zsw_setpoint_holds.csv: byte-identical yes; 3600 rows rebuilt, 0 only in the rebuild, 0 only in the release
- exclusions.json records equal as a set: yes
