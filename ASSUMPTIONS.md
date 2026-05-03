# Assumptions and Implementation Decisions

1. **Observed analytic sample**
   - The uploaded files consistently support a 253-firm included issuer sample.
   - The package therefore reproduces the workflow on 253 included issuers, not on the 546-firm figure mentioned in the user-supplied abstract.

2. **Primary evidence corpus used for variable construction**
   - The main sentence-level corpus is built from the uploaded primary evidence files:
     - `nyse_ai_python_emloyment_materials_253.csv`
     - `nyse_253_direct_company_ai_sentences.xlsx` (`All_253_Status`)
   - The filing second-coder workbook is not treated as primary corpus because no primary filing-audit workbook was uploaded.

3. **Unit of analysis**
   - The sentence is treated as the observed analytic unit because all uploaded evidence files are sentence-based.
   - The firm-level dataset aggregates these sentence records to the issuer level.

4. **Disclosure state construction**
   - `explicit_python` is assigned when any retained sentence in the primary corpus explicitly names Python.
   - `indirect_ai` is assigned when a firm has any retained public evidence sentence but no explicit Python naming.
   - `none` is assigned only when no retained evidence sentence exists in the uploaded primary corpus.
   - Because the uploaded files are evidence-positive packages, `none` is structurally rare or absent in the included 253-firm sample.

5. **Direct workbook internal conflict**
   - The `Summary` sheet in `nyse_253_direct_company_ai_sentences.xlsx` reports 252 verified and 1 closed unresolved.
   - The `README` sheet in the same workbook reports an older state of 230 filled and 23 pending.
   - The package treats the `All_253_Status` sheet and `Summary` sheet as authoritative and records the `README` inconsistency in `outputs/01_clean/workbook_notes.csv`.

6. **Second-coder direct agreement**
   - The second-coder direct workbook is used for formal agreement statistics because it overlaps the primary direct workbook on the same 253 coded units.
   - The primary direct file uses paraphrased summary sentences, while the second-coder file preserves exact or copied evidence sentences from the saved working state. Exact sentence equality is therefore reported descriptively but not interpreted as a meaningful reliability target.

7. **Filing second-coder workbook**
   - No primary filing-audit workbook was uploaded.
   - The package therefore does not compute filing-specific intercoder reliability.
   - Instead, it creates a clearly labeled proxy-alignment table comparing the filing second-coder status to a derived indicator for whether the primary direct evidence source appears to be a filing or formal report.

8. **Channel mapping**
   - Broad channel mappings are researcher-defined and implemented deterministically from observed `source_type`, `source_title`, and `source_url` fields.
   - These mappings are transparent in `config.yaml` and can be modified by future researchers.

9. **Named library dictionary**
   - The uploaded files do not include a standalone codebook of library names.
   - A transparent, minimal analytical dictionary is therefore defined in `config.yaml` from the study methodology and common Python ecosystem terms.
   - Only observed sentence matches are retained in outputs.

10. **OCI implementation**
    - OCI is implemented conservatively as a conjunction of:
      - AI or Python linkage,
      - an outcome term,
      - a quantified expression.
    - This operationalization is documented in `config.yaml` and can be tightened or relaxed by future researchers.

11. **Intensity and concentration**
    - The uploaded evidence files are already reduced to one retained sentence per firm per packaged source.
    - The resulting disclosure intensity and channel concentration measures therefore describe the uploaded packaged corpus, not the full underlying raw document universe referenced in the narrative methodology.

12. **No adjudication rules uploaded**
    - Because no adjudication protocol or resolved-final comparison file was uploaded, the package does not overwrite primary coder decisions with a synthetic adjudicated result.
    - It keeps coder-specific outputs and disagreement logs separate.
