# Code release README

Working title: Interpretable public-data validation of pretreatment mucosal modules associated with anti-TNF outcomes in inflammatory bowel disease

This code release is intended to accompany a public-database manuscript submitted to BMC Gastroenterology or a related journal. It is a cleaned scientific reproducibility package, not the journal-administration package.

## Contents

This release includes:

- analysis scripts under `scripts/`
- reproducibility documentation under `docs/`
- selected derived result tables under `results/`
- selected final figures under `results/figures/`
- supplementary table workbook under `deliverables/`
- Python package requirements in `requirements_reproducibility.txt`

This release does not include the large TAURUS GEO processed archive. That file should be downloaded from the public GEO accession:

- GSE282122: https://www.ncbi.nlm.nih.gov/geo/query/acc.cgi?acc=GSE282122

When rerunning the TAURUS 10x scoring step, place the downloaded archive in a local data directory of your choice and pass that path to the relevant script or PowerShell wrapper. Example placeholder:

```text
<LOCAL_DATA_DIR>/GSE282122_filtered_processed_data.tar.gz
```

Do not upload large raw archives to the code repository unless the chosen repository is intended for large data. Cite the public GEO/Zenodo source instead.

## Public datasets

- GSE282122: TAURUS anti-TNF single-cell atlas.
- GSE16879: mucosal expression profiling before and after first infliximab treatment.
- GSE23597: colonic biopsy expression data from infliximab-treated ulcerative colitis patients.
- GSE14580: ulcerative colitis infliximab response dataset retained as an overlap audit.

## Quick reproduction guide

See:

- `docs/reproducibility_readme.md`
- `docs/result_file_inventory.md`

The core statistical result table is:

- `results/bulk_validation/bulk_validation_enhanced_stats.csv`

The module-level summary is:

- `results/bulk_validation/bulk_validation_enhanced_module_summary.csv`

The single-cell feasibility-gate decision is:

- `results/recovery/geo_10x_full_siteaware_gate_decision.json`

## Environment

The workflow was run using Python 3.12.13. Install packages from:

```bash
pip install -r requirements_reproducibility.txt
```

The scientific analysis and figure scripts were smoke-tested in a local project virtual environment. Submission-oriented DOCX generation, final ZIP packaging and journal-administration scripts are intentionally excluded from this cleaned public package because they are not required for reproducing the scientific claims. A lightweight URL verifier (`scripts/verify_public_repository_url.py`) is retained so authors or reviewers can check the public repository/archive link recorded in manuscript materials.

## Public-package smoke test

A temporary-copy smoke test on 2026-07-19 successfully reran:

- `scripts/summarize_bulk_validation.py`
- `scripts/plot_bulk_validation_forest.py`
- `scripts/plot_workflow_schematic.py`

See `docs/public_repository_smoke_test_2026-07-19.md` for the record.

## Scientific boundary

The current release supports a public transcriptomic module-validation study. It does not support claims of:

- a clinically deployable diagnostic test;
- a causal anti-TNF resistance mechanism;
- cell-type-specific localization from the current GEO matrices alone;
- cross-lineage single-cell synchrony without annotated TAURUS H5AD files.

## Suggested citation

If using this code before publication, cite the associated manuscript title and public GEO/Zenodo datasets.

Before public deposition, fill:

- `CITATION.cff.template`

After the repository/archive URL is available, update manuscript/submission files in the separate local submission workspace. The public package itself does not include journal-finalization scripts; it only retains the standalone URL-verification helper.

## License

License to be selected by the author team before public release. Common choices:

- MIT License for code.
- CC BY 4.0 for documentation and non-code materials.

Before public deposition, complete:

- `LICENSE_DECISION_TEMPLATE.md`
- `docs/code_release_public_deposition_checklist.md`

Do not publish this repository publicly until all authors approve code/data sharing and the selected license.
