# Finance AI Public Disclosure Replication Package

This package reconstructs a deterministic Python workflow from the uploaded materials for a public-disclosure study of AI and Python signals among NYSE-listed financial issuers.

## What the package does

The pipeline:

1. Loads all uploaded raw files.
2. Validates keys, identifiers, and required columns.
3. Standardizes the issuer-screening frame, employment and technical-materials evidence, the primary direct-company evidence workbook, and the second-coder files.
4. Builds a sentence-level corpus from the uploaded primary evidence files.
5. Constructs firm-level disclosure variables, including public visibility, disclosure state, disclosure intensity, channel counts, channel concentration, named library counts, and OCI flags.
6. Uses the uploaded second-coder direct-evidence workbook for intercoder agreement, confusion matrices, and disagreement logs.
7. Uses the uploaded filing-audit second-coder workbook in a separate proxy-alignment output because no primary filing-audit workbook was uploaded.
8. Saves machine-readable outputs for every major stage and writes summary tables and figures.

## Data included in this package

The uploaded raw files are copied into `data/raw/`:

- `nyse_financial_issuer_screening.xlsx`
- `nyse_ai_python_emloyment_materials_253.csv`
- `nyse_253_direct_company_ai_sentences.xlsx`
- `nyse_253_ai_python_evidence_2nd_coder.xlsx`
- `nyse_ai_filing_evidence_audit_2nd_coder.xlsx`

## Key reproducible outputs

After running the pipeline, the package writes:

- cleaned datasets to `outputs/01_clean/`
- constructed sentence-level and firm-level datasets to `outputs/02_constructed/`
- coder agreement outputs to `outputs/03_agreement/`
- analysis tables, figures, and summary metrics to `outputs/04_analysis/`
- a run log to `logs/run_all.log`

## Important scope note

The uploaded materials support a **253-firm included issuer sample**. The package therefore reproduces the workflow on that observed sample. The user-supplied abstract references a larger frozen subset, but that larger corpus is not present in the uploaded files.

## Environment

- Python 3.11+
- Relative paths only
- Deterministic seed configured in `config.yaml`

## Installation

```bash
cd finance_ai_replication_package
python -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
```

## Run the full pipeline

```bash
python scripts/run_all.py
```

## Run tests

```bash
pytest -q
```

## Main output files

### Clean data

- `outputs/01_clean/issuer_included.csv`
- `outputs/01_clean/direct_primary.csv`
- `outputs/01_clean/employment_materials.csv`
- `outputs/01_clean/direct_second_coder.csv`
- `outputs/01_clean/filing_second_combined.csv`
- `outputs/01_clean/workbook_notes.csv`

### Constructed data

- `outputs/02_constructed/sentence_corpus.csv`
- `outputs/02_constructed/library_matches.csv`
- `outputs/02_constructed/oci_candidates.csv`
- `outputs/02_constructed/firm_level_dataset.csv`

### Agreement outputs

- `outputs/03_agreement/direct_coder_merged.csv`
- `outputs/03_agreement/direct_coder_confusion.csv`
- `outputs/03_agreement/direct_coder_metrics.csv`
- `outputs/03_agreement/direct_disagreement_log.csv`
- `outputs/03_agreement/filing_proxy_summary.csv`

### Analysis outputs

- `outputs/04_analysis/table_disclosure_state_counts.csv`
- `outputs/04_analysis/table_broad_channel_counts.csv`
- `outputs/04_analysis/table_library_dimension_summary.csv`
- `outputs/04_analysis/table_oci_summary.csv`
- `outputs/04_analysis/summary_metrics.json`
- `outputs/04_analysis/figure_disclosure_states.png`
- `outputs/04_analysis/figure_broad_channel_counts.png`
- `outputs/04_analysis/figure_channel_hhi_histogram.png`

## Methodological implementation notes

- The unit of analysis is the retained public evidence sentence in the uploaded primary evidence files.
- The firm-level dataset aggregates sentence-level evidence to the issuer level.
- The direct second-coder workbook is used for formal agreement statistics because it overlaps the primary direct-evidence workbook on the same coded units.
- The filing second-coder workbook is preserved and compared to a derived filing-source indicator from the primary direct dataset, but that output is labeled as proxy alignment rather than formal intercoder reliability because the primary filing-audit workbook was not uploaded.

## Known limitations

See `ASSUMPTIONS.md` and `TODO.md` for all documented ambiguities and unresolved issues.
