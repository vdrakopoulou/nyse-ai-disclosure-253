
# Public Technical Disclosure of AI Implementation in Finance: Python-Framed Evidence from 253 NYSE-Listed Financial Companies

**Dr Veliota Drakopoulou**  
Affiliations: (1) Higher Colleges of Technology; (2) Embry-Riddle Aeronautical University

**Zenodo archive:** [insert DOI for the 253-firm public release here].  


---

## Overview

This repository contains the replication materials for the study **“Public Technical Disclosure of AI Implementation in Finance: Python-Framed Evidence from 253 NYSE-Listed Financial Companies.”** The package reconstructs a deterministic Python workflow for a disclosure-focused study of AI- and Python-related public statements among NYSE-listed financial issuers.

The study measures **public technical disclosure**, not internal AI adoption. The package therefore focuses on what firms make visible in public materials—such as direct company sentences, employment materials, and related official sources—rather than on confidential internal systems, vendor contracts, or proprietary model inventories.

The uploaded materials support a **253-firm included issuer sample** drawn from a broader screened NYSE financial-issuer universe. The package loads the raw screening workbook, direct-company evidence workbook, employment-materials file, and second-coder files; standardizes and validates them; constructs sentence-level and firm-level datasets; generates agreement outputs; and produces machine-readable summary tables and figures.

---

## What this package reproduces

The replication workflow performs the following steps:

1. **Loads raw inputs** from the uploaded screening workbook, direct-evidence workbook, employment-materials file, and second-coder files.
2. **Validates and standardizes** issuer identifiers, subsector labels, sentence fields, source metadata, and coder-comparison variables.
3. **Builds a sentence-level corpus** from the primary uploaded evidence files.
4. **Constructs firm-level variables** including disclosure state, public visibility, disclosure intensity, channel breadth, channel concentration, named-library matches, and OCI flags.
5. **Computes coder-comparison outputs** from the uploaded second-coder direct workbook.
6. **Creates filing-proxy alignment outputs** from the uploaded filing second-coder workbook because no primary filing-audit workbook was supplied.
7. **Writes machine-readable outputs** for every stage of the workflow, together with summary tables, figures, and a run log.

This package is intended to support **reproducibility, auditability, and extension**. It is not a black-box supplement. Each stage leaves behind explicit intermediate outputs so other researchers can inspect the pipeline and modify assumptions if needed.

---

## Study frame and scope

The package is built around a **screened, exchange-bounded NYSE frame**. The raw screening workbook contains:

- **548 screened rows**
- **253 included issuers**
- **295 excluded issuers**
- **6 duplicate rows logged separately**

The broad included subsectors in the 253-firm branch are:

- Banking
- Insurance / reinsurance / title
- Diversified financial
- Consumer / specialty / mortgage finance
- Asset management / wealth
- BDC / private credit
- Broker-dealer / advisory / capital markets
- Markets infrastructure / data / payments
- Insurance brokerage / services

The package is therefore designed for a **253-firm disclosure sample**, not for the earlier 180-firm or 546-firm manuscript branches.

---

## Repository layout

```text
finance_ai_replication_package/
├── README.md
├── ASSUMPTIONS.md
├── TODO.md
├── config.yaml
├── requirements.txt
├── data/
│   └── raw/
│       ├── nyse_financial_issuer_screening.xlsx
│       ├── nyse_ai_python_emloyment_materials_253.csv
│       ├── nyse_253_direct_company_ai_sentences.xlsx
│       ├── nyse_253_ai_python_evidence_2nd_coder.xlsx
│       └── nyse_ai_filing_evidence_audit_2nd_coder.xlsx
├── scripts/
│   └── run_all.py
├── src/
│   ├── __init__.py
│   ├── utils.py
│   ├── load_data.py
│   ├── clean_data.py
│   ├── construct_variables.py
│   ├── coder_agreement.py
│   └── analysis.py
├── tests/
│   ├── conftest.py
│   ├── test_utils.py
│   ├── test_construct_variables.py
│   └── test_coder_agreement.py
├── outputs/
│   ├── 01_clean/
│   ├── 02_constructed/
│   ├── 03_agreement/
│   ├── 04_analysis/
│   └── output_manifest.csv
└── logs/
    └── run_all.log
```

---

## Raw input files

The following uploaded raw files are included under `data/raw/`:

1. **`nyse_financial_issuer_screening.xlsx`**  
   Screening workbook for the NYSE financial-issuer universe, including screened, included, excluded, and duplicate rows.

2. **`nyse_ai_python_emloyment_materials_253.csv`**  
   Employment-materials evidence file for the 253-firm branch.  
   *Note:* the filename contains the original typo `emloyment`, which is preserved for reproducibility.

3. **`nyse_253_direct_company_ai_sentences.xlsx`**  
   Primary direct-company evidence workbook, including the `All_253_Status` sheet used for construction and a `Summary` sheet used for audit counts.

4. **`nyse_253_ai_python_evidence_2nd_coder.xlsx`**  
   Second-coder direct-evidence workbook used for structured coder comparison.

5. **`nyse_ai_filing_evidence_audit_2nd_coder.xlsx`**  
   Filing-audit second-coder workbook used for proxy alignment because the corresponding primary filing-audit workbook was not uploaded.

---

## Environment and dependencies

The package is designed for:

- **Python 3.11 or later**
- relative paths only
- deterministic execution using the seed stored in `config.yaml`

To set up a clean environment:

```bash
cd finance_ai_replication_package
python -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
```

To run the full pipeline:

```bash
python scripts/run_all.py
```

To run the test suite:

```bash
pytest -q
```

---

## Pipeline stages

### Stage 1: Load raw data

`src/load_data.py` loads all raw files and required sheets listed in `config.yaml`.

### Stage 2: Clean and validate inputs

`src/clean_data.py` standardizes:

- issuer identifiers
- broad subsector labels
- direct-company evidence fields
- employment-materials records
- second-coder workbooks
- screening outcomes

It also records workbook inconsistencies in `outputs/01_clean/workbook_notes.csv`.

### Stage 3: Construct variables

`src/construct_variables.py` builds:

- the sentence-level corpus
- named-library matches
- OCI candidates
- the firm-level dataset

Core constructed variables include:

- disclosure state
- explicit Python flag
- disclosure intensity
- channel breadth
- channel concentration (HHI)
- named-library matches
- OCI flags

### Stage 4: Coder comparison

`src/coder_agreement.py` produces:

- direct-coder merged comparison files
- confusion matrices
- agreement metrics
- disagreement logs
- filing-proxy alignment outputs

### Stage 5: Analysis outputs

`src/analysis.py` generates summary tables, JSON metrics, and figures for the replication package.

---

## Main outputs

### `outputs/01_clean/`

Cleaned and standardized inputs.

Key files:

- `issuer_screened.csv`
- `issuer_included.csv`
- `issuer_excluded.csv`
- `issuer_duplicates.csv`
- `employment_materials.csv`
- `direct_primary.csv`
- `direct_second_coder.csv`
- `filing_second_verified.csv`
- `filing_second_unresolved.csv`
- `filing_second_combined.csv`
- `workbook_notes.csv`

### `outputs/02_constructed/`

Constructed analytical datasets.

Key files:

- `sentence_corpus.csv`
- `library_matches.csv`
- `oci_candidates.csv`
- `firm_level_dataset.csv`

### `outputs/03_agreement/`

Coder-comparison and disagreement outputs.

Key files:

- `direct_coder_merged.csv`
- `direct_coder_confusion.csv`
- `direct_coder_metrics.csv`
- `direct_disagreement_log.csv`
- `filing_proxy_merged.csv`
- `filing_proxy_summary.csv`

### `outputs/04_analysis/`

Machine-readable tables, figures, and summary metrics.

Key files:

- `table_issuer_screening_counts.csv`
- `table_disclosure_state_counts.csv`
- `table_broad_channel_counts.csv`
- `table_dataset_channel_counts.csv`
- `table_python_mentions_by_dataset_channel.csv`
- `table_direct_source_type_counts.csv`
- `table_named_library_counts.csv`
- `table_library_dimension_summary.csv`
- `table_channel_hhi_summary.csv`
- `table_intensity_summary.csv`
- `table_subsector_state_counts.csv`
- `table_oci_summary.csv`
- `summary_metrics.json`
- `figure_disclosure_states.png` / `.pdf`
- `figure_broad_channel_counts.png` / `.pdf`
- `figure_channel_hhi_histogram.png` / `.pdf`

---

## Core package-level results reproduced by the pipeline

The deterministic package outputs reproduce the following high-level metrics from `summary_metrics.json` and the analysis tables:

- **253 included firms** in the analytical sample
- **34 explicit Python firms**
- **219 indirect AI firms**
- **1 OCI-positive firm**
- **1 OCI-positive sentence**
- **505 retained sentences** in the combined sentence corpus
- **65.2% raw agreement** for direct-evidence coder comparison
- **Cohen’s kappa = 0.015** for the direct-evidence comparison
- **Gwet’s AC1 = 0.508** for the direct-evidence comparison

Broad channel counts in the sentence corpus are:

- 130 corporate-communications sentences
- 123 employment-materials sentences
- 106 filings/formal-report sentences
- 73 press/news sentences
- 64 technical-documentation sentences
- 9 investor-materials sentences

Named-library matches retained in the package include:

- `spark`
- `pyspark`
- `scikit-learn`
- `dash`
- `plotly`
- `fastapi`

The OCI summary table reports a firm-level prevalence of approximately **0.40%** and a one-sided 95% upper bound of approximately **1.86%**.

---

## Important note on package-level counts versus manuscript-facing counts

This repository preserves the **full deterministic replication workflow**, not just the compact manuscript-facing results layer. Because of that, some counts in the package may differ from the stricter manuscript tables.

### Package-level analytical layer

The constructed `firm_level_dataset.csv` uses the uploaded primary evidence files as the core observed corpus. Under that deterministic construction, all 253 included firms are evidence-positive, which yields:

- **34 `explicit_python` firms**
- **219 `indirect_ai` firms**
- **0 `none` firms**

### Manuscript-facing compact layer

The manuscript-facing compact results layer applies a **stricter official-source release rule**. Under that stricter rule, the counts may be reported as:

- **34 Explicit Python**
- **216 Indirect AI**
- **3 None**

Those three residual cases arise from the release audit rather than from the broader package-level evidence construction. In the direct workbook and release audit, the relevant status counts are:

- **252 verified direct company sentences** and **1 closed unresolved** in the direct-evidence summary
- **250 ready valid official sentences**, **2 replacement-required nonofficial cases**, and **1 unresolved no-strict-direct-match case** in the strict release layer

In other words, the full package and the compact manuscript tables answer slightly different questions:

- the **package-level dataset** preserves the broader observed evidence-positive corpus;
- the **manuscript-facing compact layer** enforces a stricter release-quality official-source standard.

Both are useful, but they should not be treated as interchangeable without noting the rule difference.

---

## Agreement outputs and how to interpret them

The package includes two distinct coder-comparison layers.

### Direct second-coder comparison

This is the formal coder-comparison layer because it overlaps the primary direct-company workbook on the same 253 units.

Key outputs:

- `direct_coder_metrics.csv`
- `direct_coder_confusion.csv`
- `direct_disagreement_log.csv`

Important interpretation note:

The primary direct workbook uses paraphrased summary sentences, while the second-coder workbook often preserves exact or copied evidence sentences. For that reason, **exact sentence equality is descriptive only** and should not be treated as the main reliability target.

### Filing second-coder proxy alignment

The filing second-coder workbook is preserved, but because no primary filing-audit workbook was uploaded, the package does **not** compute filing-specific intercoder reliability. Instead, it creates a proxy-alignment comparison based on whether the selected primary direct source appears to be a filing or formal report.

Key outputs:

- `filing_proxy_merged.csv`
- `filing_proxy_summary.csv`

These outputs are clearly labeled as **proxy alignment**, not formal intercoder reliability.

---

## Configuration and reproducibility choices

Key implementation rules are stored in `config.yaml`, including:

- file paths
- workbook sheet names
- AI regex patterns
- OCI outcome and quantity regex patterns
- library-context rules
- broad-channel mapping rules
- named-library dictionary
- output directories
- random seed (`20260428`)

This design allows future researchers to:

- tighten or relax the OCI rule
- modify channel mappings
- expand the library dictionary
- rerun the pipeline with alternative assumptions

---

## Assumptions and known limitations

The package documents its main assumptions in `ASSUMPTIONS.md` and open items in `TODO.md`.

Important limitations include:

1. The package supports a **253-firm included issuer sample**, not the earlier 546-firm or 180-firm branches.
2. The sentence-level corpus is built from the uploaded primary evidence files only.
3. The filing second-coder workbook cannot be used for formal intercoder reliability because the corresponding primary filing-audit workbook was not uploaded.
4. Channel mappings are deterministic research decisions defined in `config.yaml`.
5. The named-library dictionary is intentionally minimal and transparent.
6. OCI is implemented conservatively as a conjunction of:
   - AI/Python linkage,
   - an outcome term,
   - a quantified expression.
7. The uploaded evidence files are already reduced artifacts, not the full underlying raw document universe.
8. No adjudication log was uploaded, so the package does not synthesize an adjudicated final coder file.

Open TODO items include:

- adding the full raw document corpus
- adding the primary filing-audit workbook
- adding an adjudication log
- adding a formal codebook
- adding omitted sectoral-press materials if available
- adding exact publication-formatted tables if required

---

## Suggested use in a manuscript or review package

This package is best used for:

- reproducing the 253-firm analytical workflow
- auditing how the sentence corpus and firm-level dataset were built
- inspecting coder disagreements and release-audit issues
- regenerating machine-readable tables and figures
- supporting methods, reproducibility, and robustness sections

If you are writing the manuscript itself, it is helpful to distinguish between:

- the **full replication package** (this repository), and
- the **compact manuscript-facing results layer** used for final journal tables.

That distinction should be stated explicitly wherever package-level and manuscript-level counts differ.

---

## How to cite this package

If the 253-firm branch receives its own Zenodo DOI, cite that archived release directly. If not, and this package corresponds to the manuscript’s current public archive, update the citation line accordingly.

Suggested citation format:

> Drakopoulou, V. (2026). *Public Technical Disclosure of AI Implementation in Finance: Python-Framed Evidence from 253 NYSE-Listed Financial Companies* [Replication package]. Zenodo. [DOI]

---

## Contact

**Dr Veliota Drakopoulou**  
Higher Colleges of Technology  
Embry-Riddle Aeronautical University

For questions about the replication materials, variable construction, or release-layer interpretation, consult the package documentation first (`README.md`, `ASSUMPTIONS.md`, `TODO.md`, `config.yaml`) and then the manuscript methods section.

---

## Quick-start checklist

- [ ] Create and activate a Python environment
- [ ] Install dependencies with `pip install -r requirements.txt`
- [ ] Run `python scripts/run_all.py`
- [ ] Inspect `logs/run_all.log`
- [ ] Review outputs in `outputs/01_clean/` through `outputs/04_analysis/`
- [ ] Check `ASSUMPTIONS.md` before comparing counts to manuscript tables
- [ ] Document whether you are using the **package-level analytical layer** or the **strict manuscript-facing release layer**
