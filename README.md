# Code release README

Working title: Interpretable public-data validation of pretreatment mucosal modules associated with anti-TNF outcomes in inflammatory bowel disease

This repository accompanies a public-database transcriptomic analysis of pretreatment mucosal modules associated with anti-TNF outcomes in inflammatory bowel disease. It is a cleaned scientific reproducibility package, not the journal-administration package.

## Public datasets

- GSE282122: TAURUS anti-TNF single-cell atlas.
- GSE16879: mucosal expression profiling before and after first infliximab treatment.
- GSE23597: colonic biopsy expression data from infliximab-treated ulcerative colitis patients.
- GSE14580: ulcerative colitis infliximab response dataset retained as an overlap audit.

## Quick reproduction guide

The prepared public-release archive is `public_repository_ready_v2.zip` in the local submission workspace. The repository will contain analysis scripts, reproducibility documentation, selected derived results, figures, and requirements.

The large TAURUS GEO processed archive is not included. It should be downloaded from public GEO accession GSE282122: https://www.ncbi.nlm.nih.gov/geo/query/acc.cgi?acc=GSE282122

## Environment

The workflow was run using Python 3.12.13. Install packages from `requirements_reproducibility.txt`.

## Scientific boundary

The current release supports a public transcriptomic module-validation study. It does not support claims of a clinically deployable diagnostic test, a causal anti-TNF resistance mechanism, cell-type-specific localization from the current GEO matrices alone, or cross-lineage single-cell synchrony without annotated TAURUS H5AD files.

## License

License to be selected by the author team before public release. Common choices are MIT License for code and CC BY 4.0 for documentation and non-code materials.
