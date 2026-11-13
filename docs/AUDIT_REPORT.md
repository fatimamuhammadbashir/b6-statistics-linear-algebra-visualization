# B6 Final Audit Report

**Project:** Statistics, Linear Algebra Intuition, and Visualization  
**Folder:** `FIP-B4-B5/B6`  
**Audit date:** 2026-11-13  
**Audit type:** read-only verification of the completed project  
**Overall verdict:** **PASS — all official and quality requirements are met.** No blocking issues found. The assignment has **not** been submitted.

---

## 1. Audit summary

| Area | Result |
|---|---|
| Official deliverables (9) | 9 / 9 PASS |
| Quality requirements (10) | 10 / 10 PASS |
| Notebook execution | PASS — 14 / 14 code cells executed, 0 cell errors, return code 0 |
| Charts | PASS — 7 meaningful, labelled PNG charts (requirement: at least 4) |
| Spreadsheet cross-check | PASS — 25 / 25 checks, maximum absolute difference 1.22 × 10⁻¹⁵ |
| Written insights | PASS — 5 insights, each supported by computed data |
| Dataset provenance | PASS — Kaggle source, upstream UCI record, licence and checksums documented |
| B4 / B5 isolation | PASS — no files created, edited or deleted in either folder |
| Git / publishing | PASS — no repository initialized in B6 or its parent; nothing committed or pushed |
| Submission | Not submitted — awaiting user approval |

**Files in B6 after this report:** 32 (31 project artifacts + this audit report).

---

## 2. Dataset source and licence

| Item | Detail |
|---|---|
| Kaggle dataset | **Student Alcohol Consumption** |
| Kaggle URL | https://www.kaggle.com/datasets/uciml/student-alcohol-consumption |
| Kaggle owner / uploader | UCI Machine Learning / Dmitrii Batogov |
| Kaggle version | 2 (last updated 2016-10-19 per Kaggle API metadata) |
| Kaggle licence label | **CC0: Public Domain** |
| Upstream dataset | **Student Performance**, UCI Machine Learning Repository, ID 320 |
| Upstream URL | https://archive.ics.uci.edu/dataset/320/student+performance |
| Upstream DOI | https://doi.org/10.24432/C5TG7T |
| Upstream licence | **CC BY 4.0** |
| Creators | Paulo Cortez and António M. G. Silva (University of Minho, 2008) |
| Files archived | `student-mat.csv` (395 × 33), `student-por.csv` (649 × 33), `student-merge.R` |

The Kaggle mirror is the required Kaggle source. Because the original UCI dataset is CC BY 4.0, attribution to Cortez and Silva is retained even though the Kaggle mirror is labelled CC0. Full provenance is in `data/raw/SOURCE.md`.

**Raw-file integrity.** The archived CSVs are byte-for-byte copies of the Kaggle extraction and are verified by SHA-256 at the start of every notebook run:

| File | SHA-256 |
|---|---|
| `student-mat.csv` | `659F3984643C2DEF53BA5E49F551C6CE3657039F9C25306CACB8F43B818A5190` |
| `student-por.csv` | `3FB408FE4B66D4CDB90AD4EC5E3FB6DE94BA662D0471A3D46C03DA483069F76B` |

No data were invented, synthesised, scraped from an undocumented source, or altered.

---

## 3. Official requirements — PASS/FAIL

| # | Official requirement | Result | Evidence |
|---:|---|---|---|
| 1 | Jupyter notebook with complete analysis | **PASS** | `notebooks/FIP_B6_analysis.ipynb` — 41 cells (27 markdown, 14 code), executed in place, outputs saved |
| 2 | Original dataset and documented Kaggle source link | **PASS** | Raw CSVs, original `student-merge.R`, `data/raw/SOURCE.md`; Kaggle URL and UCI DOI documented |
| 3 | Statistical summary | **PASS** | Notebook §4; `data/processed/summary_statistics.csv`, `cohort_summary.csv` |
| 4 | Correlation analysis | **PASS** | Notebook §9; Pearson and Spearman matrices, tests, bootstrap CIs, BH correction; `data/processed/correlation_*.csv`; Figure 5 |
| 5 | At least four meaningful charts | **PASS** | 7 charts in `charts/` (see §6) |
| 6 | Spreadsheet cross-check of selected calculations | **PASS** | `spreadsheet/B6_statistics_crosscheck.xlsx` with live formulas; `spreadsheet/crosscheck_results.csv`; `docs/CROSSCHECK.md`; 25/25 PASS |
| 7 | Five written insights supported by actual data | **PASS** | Notebook §11; `docs/INSIGHTS.md`; each insight cites computed statistics |
| 8 | Chart critique guide | **PASS** | `docs/CHART_CRITIQUE_GUIDE.md` — 10 sections, review template, rubric, reviews of all 7 charts |
| 9 | README with setup and execution instructions | **PASS** | `README.md` — setup, run commands, deliverable map, structure, methods, limitations, troubleshooting |

### Task coverage

| Task element | Result | Where addressed |
|---|---|---|
| Score distributions | **PASS** | Notebook §5 and Figure 1; ECDF/histograms; cohort level, spread and lower tail |
| Attendance patterns | **PASS** | Notebook §6 and Figure 2; zero-inflation, band means, correlations, CIs |
| Sampling differences | **PASS** | Notebook §8 and Figure 4; composition, school stratification, overlap analysis, bias discussion |
| Study habits and results | **PASS** | Notebook §7 and Figure 3; study time, failures, paid classes, aspiration |
| Correlation and its limitations | **PASS** | Notebook §9; effect sizes, intervals, multiplicity, six explicit limits |
| Vectors, matrices, similarity intuition | **PASS** | Notebook §10 and Figures 6–7; worked dot product, norms, cosine, Gram matrix, projection, R² = cos²θ |

---

## 4. Quality requirements — PASS/FAIL

| # | Quality requirement | Result | Evidence |
|---:|---|---|---|
| 1 | Reproducible Python code | **PASS** | Fixed seed `20261113`, relative path resolution, pinned `requirements.txt`, checksum assertions, deterministic data pipeline |
| 2 | Label every chart clearly | **PASS** | Every figure has takeaway title, subtitle defining encoding/sample, axis labels with units, legend, and source note; all 7 visually checked |
| 3 | Explain what each chart shows | **PASS** | A “What Figure N shows” interpretation follows every figure; also reviewed in the critique guide |
| 4 | Explain why correlation does not prove causation | **PASS** | Notebook §9 gives six dataset-specific reasons; reinforced in Insights 2 and 5 and the critique guide |
| 5 | Document missing values and cleaning decisions | **PASS** | Notebook §3; `data/processed/cleaning_decisions.csv`; `docs/DATA_DICTIONARY.md`; README §7 |
| 6 | Explain sampling limitations and possible bias | **PASS** | Notebook §8 and §13; convenience sample, two schools, cohort composition, selection into paid tuition/school/subject, many-to-many overlap |
| 7 | Explain vectors, matrices, similarity with simple dataset examples | **PASS** | Notebook §10; MAT-001 vs MAT-019 worked example; 1,044 × 5 matrix; Gram/correlation matrix; cosine-similarity heatmap; least-squares projection |
| 8 | Cross-check selected statistics with spreadsheet-compatible files | **PASS** | Live-formula `.xlsx`; 25 selected checks; independent Python comparison; 25/25 PASS at 1 × 10⁻⁹ tolerance |
| 9 | Never fabricate findings | **PASS** | All quoted values trace to notebook computations or processed CSVs; sources and checksums documented; limitations stated rather than hidden |
| 10 | Ensure notebook runs beginning to end | **PASS** | Clean `nbconvert` run, return code 0, 14/14 code cells executed, 0 cell errors; log in `outputs/notebook_execution.log` |

**Tooling requirement.** Python 3.13.17, pandas 3.1.1, NumPy 2.5.4, Matplotlib 3.11.2, Seaborn 0.13.2, SciPy 1.18.1, Jupyter/nbconvert, openpyxl and the free `formulas` 1.3.4 engine. All tools are free/open source; no proprietary software is required.

---

## 5. Notebook execution status

| Item | Result |
|---|---|
| Notebook path | `notebooks/FIP_B6_analysis.ipynb` |
| Total cells | 41 |
| Markdown cells | 27 |
| Code cells | 14 |
| Executed code cells | **14 / 14** |
| Cell errors | **0** |
| Return code | **0** |
| Execution date | 2026-11-13 15:43 (local) |
| Kernel | `b6-venv` (Python 3.13.17) |
| Execution command | `jupyter-nbconvert --to notebook --execute --inplace --ExecutePreprocessor.timeout=900 --ExecutePreprocessor.kernel_name=b6-venv notebooks/FIP_B6_analysis.ipynb` |
| Log | `outputs/notebook_execution.log` |

The notebook executes top-to-bottom from a clean kernel. It recreates all processed tables, all 7 charts, the spreadsheet workbook, the cross-check CSV and the environment-version record. The execution log shows `Result: PASS — notebook executed end-to-end with zero cell errors`.

**Note on the execution log.** It records two benign environment warnings (a Windows ZMQ event-loop warning and a local-kernel TCP-without-encryption notice). Neither is a notebook cell error; the kernel completed normally with return code 0.

---

## 6. Charts — 7 delivered (requirement: ≥ 4)

| # | File | What it communicates |
|---:|---|---|
| 1 | `charts/01_grade_distributions.png` | G3 histogram/density and ECDF by cohort; level, spread and the mathematics zero spike |
| 2 | `charts/02_attendance_patterns.png` | Zero-inflated absences; band means with 95% CIs; weak, non-monotonic grade–absence pattern |
| 3 | `charts/03_study_habits_grades.png` | Mean G3 by study-time band and by past failures, with 95% CIs |
| 4 | `charts/04_sampling_comparison.png` | Cohort composition differences and subject × school grade means |
| 5 | `charts/05_correlation_heatmap.png` | Separate Spearman correlation matrices for Mathematics and Portuguese |
| 6 | `charts/06_vector_similarity.png` | Cosine-similarity matrix for 60 ordered students; mean similarity by grade distance |
| 7 | `charts/07_projection_g2_g3.png` | G3 vs G2 with least-squares projection; annotated `r`, `R²` and angle |

All are 200-dpi PNGs, use a colourblind-safe blue/vermillion palette, and carry titles, subtitles, axis labels, units, sample sizes or group counts, and source notes. Label collisions identified during visual review were corrected before the final execution.

---

## 7. Spreadsheet cross-check

| Item | Result |
|---|---|
| Workbook | `spreadsheet/B6_statistics_crosscheck.xlsx` |
| Sheets | `README`, `Math_Data`, `Por_Data`, `Summary`, `Correlations`, `Group_Means`, `Similarity`, `Comparison` (8 sheets) |
| Formula types | `COUNT`, `AVERAGE`, `MEDIAN`, `STDEV`, `MIN`, `MAX`, `QUARTILE.INC`, `COUNTIF`, `AVERAGEIF`, `CORREL`, `SUMPRODUCT`, `SUMSQ`, `SQRT`, `ABS`, `IF` |
| Selected checks | 25 |
| Checks passed | **25 / 25** |
| Tolerance | 1 × 10⁻⁹ |
| Maximum absolute difference | **1.2212453270876722 × 10⁻¹⁵** |
| Recalculation engine | Free `formulas` 1.3.4 (no Excel or LibreOffice installed) |
| Machine-readable result | `spreadsheet/crosscheck_results.csv` |
| Narrative record | `docs/CROSSCHECK.md` |

The checks cover per-cohort n, mean, median, sample SD and pass rate for G3; Pearson correlations of G3 with G2 and absences; all four study-time band means per cohort; and raw/centred cosine similarity plus Euclidean distance for MAT-001 vs MAT-019. These are selective checks of the pipeline and arithmetic, not a re-derivation of every notebook number; that scope is stated in the documentation.

The workbook formulas are live and will recalculate in Excel or LibreOffice. `formulas` was used so the check is reproducible without proprietary software.

---

## 8. Five written insights

All five are in `docs/INSIGHTS.md` and notebook §11, with tables and caveats. Summary:

1. **Final grades differ by cohort in level, spread and lower tail.** Mathematics mean 10.42 (SD 4.58) vs Portuguese 11.91 (SD 3.23); 9.6% vs 2.3% scored zero; 67.1% vs 84.6% passed.
2. **Attendance is weakly related to grades and not monotonically.** Pearson r = +0.034 (Mathematics, p = 0.497), −0.091 (Portuguese, p = 0.020), pooled −0.046 (bootstrap 95% CI −0.103 to +0.009); zero-absence mathematics students average only 8.44.
3. **Study time tracks grades more clearly in Portuguese; past failures track them in both.** Spearman ρ = 0.105 vs 0.275 for study time; ρ = −0.361 vs −0.448 for failures.
4. **The cohorts are different samples, so the raw gap is not a subject effect.** MS share 11.6% vs 34.8%; paid classes 45.8% vs 6.0%; school-mix-standardised gap 1.75 points vs raw 1.49; 382 approximate matches are many-to-many (187 distinct mathematics grade triples).
5. **Prior grade dominates, and correlation does not establish causation.** G2–G3 r = 0.905 / 0.919 (R² = 0.819 / 0.844); adding absences, study time and failures raises R² only to 0.826 / 0.847; paid-tuition differences are non-significant but heavily selected.

Each insight includes an explicit caveat about confounding, reverse causality, measurement limits or selection. No causal claim is made from observational data.

---

## 9. Files created

**Total: 32 files** (31 before this report + `docs/AUDIT_REPORT.md`).

### Root
- `README.md`
- `requirements.txt`

### Data
- `data/raw/SOURCE.md`
- `data/raw/student-mat.csv`
- `data/raw/student-merge.R`
- `data/raw/student-por.csv`
- `data/processed/attendance_by_band.csv`
- `data/processed/cleaning_decisions.csv`
- `data/processed/cohort_summary.csv`
- `data/processed/correlation_pearson_math.csv`
- `data/processed/correlation_pearson_portuguese.csv`
- `data/processed/correlation_spearman_math.csv`
- `data/processed/correlation_spearman_portuguese.csv`
- `data/processed/correlation_tests_pooled.csv`
- `data/processed/summary_statistics.csv`

### Notebook
- `notebooks/FIP_B6_analysis.ipynb`

### Charts
- `charts/01_grade_distributions.png`
- `charts/02_attendance_patterns.png`
- `charts/03_study_habits_grades.png`
- `charts/04_sampling_comparison.png`
- `charts/05_correlation_heatmap.png`
- `charts/06_vector_similarity.png`
- `charts/07_projection_g2_g3.png`

### Spreadsheet
- `spreadsheet/B6_statistics_crosscheck.xlsx`
- `spreadsheet/crosscheck_results.csv`

### Documentation
- `docs/AUDIT_REPORT.md` (this report)
- `docs/CHART_CRITIQUE_GUIDE.md`
- `docs/CROSSCHECK.md`
- `docs/DATA_DICTIONARY.md`
- `docs/INSIGHTS.md`

### Outputs
- `outputs/environment_versions.csv`
- `outputs/notebook_execution.log`

### 9.1 Authoritative file list (32)

```text
README.md
requirements.txt
charts/01_grade_distributions.png
charts/02_attendance_patterns.png
charts/03_study_habits_grades.png
charts/04_sampling_comparison.png
charts/05_correlation_heatmap.png
charts/06_vector_similarity.png
charts/07_projection_g2_g3.png
data/processed/attendance_by_band.csv
data/processed/cleaning_decisions.csv
data/processed/cohort_summary.csv
data/processed/correlation_pearson_math.csv
data/processed/correlation_pearson_portuguese.csv
data/processed/correlation_spearman_math.csv
data/processed/correlation_spearman_portuguese.csv
data/processed/correlation_tests_pooled.csv
data/processed/summary_statistics.csv
data/raw/SOURCE.md
data/raw/student-mat.csv
data/raw/student-merge.R
data/raw/student-por.csv
docs/AUDIT_REPORT.md
docs/CHART_CRITIQUE_GUIDE.md
docs/CROSSCHECK.md
docs/DATA_DICTIONARY.md
docs/INSIGHTS.md
notebooks/FIP_B6_analysis.ipynb
outputs/environment_versions.csv
outputs/notebook_execution.log
spreadsheet/B6_statistics_crosscheck.xlsx
spreadsheet/crosscheck_results.csv
```

---

## 10. Missing requirements or issues

**Missing official requirements:** none.  
**Failing quality requirements:** none.  
**Blocking issues:** none.

### Non-blocking observations

1. **No Excel or LibreOffice was installed.** The workbook therefore was recalculated with the free `formulas` 1.3.4 engine rather than the desktop application. This is documented and reproducible; the workbook remains Excel/LibreOffice-compatible with live formulas.
2. **Benign execution warnings.** The `nbconvert` log contains a Windows ZMQ event-loop warning and a local-kernel TCP notice. There were zero notebook cell errors and return code 0.
3. **Selective cross-check.** The spreadsheet validates 25 representative statistics, not every number in the notebook. This scope is stated openly in `docs/CROSSCHECK.md` and the notebook.
4. **Small subgroups.** Some failure/study-time cells contain 14–35 students and have wide confidence intervals. This is disclosed in the notebook and chart critique.
5. **Many-to-many cohort overlap.** The original merge keys produce 382 matched rows but only 187 distinct mathematics grade triples. The project explicitly does not treat this as a paired panel and keeps cohorts separate for inference.

None of these observations changes a PASS verdict.

---

## 11. B4 and B5 — confirmation

No files in sibling folders `../B4` or `../B5` were created, edited, moved or deleted during this B6 build. The audit was read-only outside B6.

| Folder | LastWriteTime | Status |
|---|---|---|
| `B4` | `11/12/2026 12:14:49 PM` | Unchanged from the pre-build value |
| `B5` | `11/12/2026 6:47:27 PM` | Unchanged from the pre-build value |

B4 and B5 each contain their own `.git` directory. No Git commands were run inside either folder, and their repositories were not touched.

---

## 12. Git and publishing — confirmation

| Check | Result |
|---|---|
| `.git` in project root (`B6`) | **Does not exist** |
| `.git` in parent (`..`) | **Does not exist** |
| `git rev-parse --is-inside-work-tree` from B6 | Fails with exit code **128** (not a Git repository) |
| Repository initialized | **No** |
| Commit created | **No** |
| Push performed | **No** |
| Package/file published | **No** |
| Assignment submitted | **No** |

Git was not initialized, no commit was made, nothing was pushed, and nothing was published. The project is a plain folder awaiting review.

---

## 13. Final verdict

**B6 is complete and passes the audit against every official and quality requirement.**

- 9 / 9 official requirements PASS
- 10 / 10 quality requirements PASS
- Notebook executed end-to-end with 0 errors
- 7 charts delivered and reviewed
- 25 / 25 spreadsheet checks PASS
- 5 data-supported insights delivered
- Dataset source, licence and checksums documented
- B4 and B5 untouched
- No Git, no commit, no push, no publication
- Assignment not submitted

**Status: awaiting user approval. No further action will be taken until then.**
