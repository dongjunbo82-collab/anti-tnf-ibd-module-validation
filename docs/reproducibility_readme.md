# Reproducibility README

Project: public-database mucosal module analysis of anti-TNF outcomes in inflammatory bowel disease

Last updated: 2026-07-19

## What this repository/package contains

This project contains scientific-analysis scripts, derived tables, figures and reproducibility documentation for a public-database analysis of pretreatment mucosal modules associated with anti-TNF outcomes in IBD.

The analysis has two major evidence tracks:

1. TAURUS/GSE282122 feasibility gate: verifies public single-cell data availability, supports whole-biopsy module scoring and defines the boundary of analyses based on GEO processed matrices.
2. Bulk validation: tests prespecified mucosal modules across GSE16879 and GSE23597, with GSE14580 retained as an overlap audit rather than independent validation.

## Recommended environment

The analysis was run locally on Windows using Python 3.12.13.

Observed package versions:

- pandas 3.0.3
- numpy 2.5.1
- scipy 1.18.0
- h5py 3.16.0
- matplotlib 3.11.0
- seaborn 0.13.2
- statsmodels 0.14.6
- scikit-learn 1.9.0
- anndata 0.13.1

Install package requirements from `requirements_reproducibility.txt`. A local virtual environment such as `.venv` can be used, but it is not included in the release.

The scientific analysis and figure scripts were smoke-tested from a temporary copy of `public_repository_ready_v2` on 2026-07-19 using the local project virtual environment. The test reran `scripts/summarize_bulk_validation.py`, `scripts/plot_bulk_validation_forest.py` and `scripts/plot_workflow_schematic.py`.

## External data locations

Large input data are stored outside the project directory and must be downloaded from public repositories. For the TAURUS processed GEO archive, use a local path of your choice, for example:

- `<LOCAL_DATA_DIR>/GSE282122_filtered_processed_data.tar.gz`

Public data sources:

- GSE282122: https://www.ncbi.nlm.nih.gov/geo/query/acc.cgi?acc=GSE282122
- TAURUS Zenodo record: https://zenodo.org/records/14007626
- GSE16879: https://www.ncbi.nlm.nih.gov/geo/query/acc.cgi?acc=GSE16879
- GSE23597: https://www.ncbi.nlm.nih.gov/geo/query/acc.cgi?acc=GSE23597
- GSE14580: https://www.ncbi.nlm.nih.gov/geo/query/acc.cgi?acc=GSE14580

Important limitation: the reproducibility-critical workflow in this package uses GEO processed 10x matrices and does not require annotated TAURUS H5AD objects. Therefore, current single-cell claims are limited to GEO 10x whole-biopsy matrix scoring and feasibility gating rather than annotated lineage-level cell-state localization.

## Reproduction order

### 1. TAURUS metadata and archive feasibility

```powershell
python scripts\parse_gse282122_soft.py
python scripts\audit_umap_sample_coverage.py
python scripts\audit_gse282122_processed_tar.py
```

### 2. TAURUS whole-biopsy module scoring and recovery gate

```powershell
powershell -ExecutionPolicy Bypass -File scripts\run_geo_10x_full_gate.ps1
```

Main underlying scripts:

```powershell
python scripts\score_10x_h5_modules_from_tar.py
python scripts\compute_recovery_synchrony.py --pair-by-site
python scripts\summarize_recovery_gate.py
python scripts\plot_recovery_synchrony.py
```

Interpretation: whole-biopsy recovery was computable but weak and not suitable as the primary positive result.

### 3. Bulk GEO validation

```powershell
python scripts\download_geo_series_matrix.py
python scripts\score_bulk_series_matrix_modules.py
python scripts\analyze_gse16879_bulk_modules.py
python scripts\analyze_gse23597_bulk_modules.py
python scripts\summarize_bulk_validation.py
python scripts\enhance_bulk_validation_stats.py
python scripts\audit_bulk_module_score_sensitivity.py
```

Key outputs:

- `results/bulk_validation/GSE16879_bulk_module_tests.csv`
- `results/bulk_validation/GSE23597_bulk_module_tests.csv`
- `results/bulk_validation/GSE14580_bulk_module_tests.csv`
- `results/bulk_validation/bulk_validation_enhanced_stats.csv`
- `results/bulk_validation/bulk_validation_enhanced_module_summary.csv`
- `results/bulk_validation/bulk_module_score_sensitivity_summary.json`

Interpretation: GSE16879 and GSE23597 support the pretreatment module-response association. GSE14580 overlaps with GSE16879 UC results and should not be counted as an independent validation cohort.

### 4. Figure generation

```powershell
python scripts\plot_workflow_schematic.py
python scripts\plot_gse16879_bulk_validation.py
python scripts\plot_gse23597_bulk_validation.py
python scripts\plot_bulk_validation_forest.py
python scripts\plot_recovery_synchrony.py
python scripts\plot_feasibility_coverage.py
```

## Primary result files for manuscript claims

- Main cross-cohort statistics: `results/bulk_validation/bulk_validation_enhanced_stats.csv`
- Module summary: `results/bulk_validation/bulk_validation_enhanced_module_summary.csv`
- Sensitivity summary: `results/bulk_validation/bulk_module_score_sensitivity_summary.json`
- TAURUS feasibility-gate decision: `results/recovery/geo_10x_full_siteaware_gate_decision.json`
- Supplementary table workbook supplied as a derived output: `deliverables/supplementary_tables_v1.xlsx`

## Claims supported by current outputs

Supported:

- Pretreatment mucosal module activity is associated with later anti-TNF response in public IBD cohorts.
- Myeloid inflammation is the most consistent module, lower in responders across all independent comparisons and meeting FDR q < 0.10 in all tested strata.
- TAURUS whole-biopsy module scoring is feasible, but whole-biopsy recovery toward healthy is not robust enough as a primary response metric.
- GSE14580 should be treated as an overlap audit rather than an independent validation cohort.

Not supported without further data:

- A clinically deployable diagnostic test.
- A new causal anti-TNF resistance mechanism.
- Cell-type-specific single-cell localization.
- Cross-lineage recovery synchrony from the current GEO matrices alone.

## Suggested public repository contents

If the authors decide to create a public repository, include `scripts/`, `docs/`, selected `results/`, final figure exports and `deliverables/supplementary_tables_v1.xlsx`.

Do not upload very large raw archives unless the repository is designed for large data. Instead, cite GEO/Zenodo accessions and document the expected external data path with a placeholder such as `<LOCAL_DATA_DIR>`.
