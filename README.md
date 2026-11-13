# FIP B6 — Statistics, Linear Algebra Intuition, and Visualization

An independent, reproducible analysis of student performance in two Portuguese
secondary-school cohorts. The project uses Python, pandas, Matplotlib/Seaborn and a
Jupyter notebook, and it cross-checks selected statistics in a spreadsheet-compatible
workbook.

**Dataset:** Kaggle *Student Alcohol Consumption* (a mirror of the UCI *Student
Performance* dataset by Cortez & Silva, 2008).
**Sample:** 1,044 students — Mathematics (n = 395) and Portuguese language (n = 649).
**Repository:** [b6-statistics-linear-algebra-visualization](https://github.com/fatimamuhammadbashir/b6-statistics-linear-algebra-visualization) — public GitHub repository.
**Status:** notebook executed end-to-end with zero errors; 7 charts; 25/25 spreadsheet
cross-checks PASS. FIP submission is still pending.

---

## 1. What is in this project

| Official requirement | Where it is delivered |
|---|---|
| Jupyter notebook with complete analysis | `notebooks/FIP_B6_analysis.ipynb` (executed, outputs saved) |
| Original dataset + documented Kaggle source | `data/raw/student-mat.csv`, `data/raw/student-por.csv`, `data/raw/student-merge.R`, `data/raw/SOURCE.md` |
| Statistical summary | Notebook §4; `data/processed/summary_statistics.csv`, `data/processed/cohort_summary.csv` |
| Correlation analysis | Notebook §9; `data/processed/correlation_*.csv`; `charts/05_correlation_heatmap.png` |
| At least four meaningful charts | 7 charts in `charts/` (see §8) |
| Spreadsheet cross-check | `spreadsheet/B6_statistics_crosscheck.xlsx`; `spreadsheet/crosscheck_results.csv`; `docs/CROSSCHECK.md` |
| Five written insights supported by data | Notebook §11; `docs/INSIGHTS.md` |
| Chart critique guide | `docs/CHART_CRITIQUE_GUIDE.md` |
| README with setup and execution | This file |
| Data dictionary / cleaning record | `docs/DATA_DICTIONARY.md`; `data/processed/cleaning_decisions.csv` |
| Reproducibility record | `outputs/notebook_execution.log`, `outputs/environment_versions.csv` |

## 2. Project structure

```text
B6/
├── README.md
├── requirements.txt
├── data/
│   ├── raw/
│   │   ├── SOURCE.md                 # Kaggle URL, UCI DOI, licence, checksums
│   │   ├── student-mat.csv           # original Kaggle file, unmodified
│   │   ├── student-por.csv           # original Kaggle file, unmodified
│   │   └── student-merge.R           # original archive helper (reference only)
│   └── processed/
│       ├── summary_statistics.csv
│       ├── cohort_summary.csv
│       ├── cleaning_decisions.csv
│       ├── attendance_by_band.csv
│       ├── correlation_pearson_math.csv
│       ├── correlation_pearson_portuguese.csv
│       ├── correlation_spearman_math.csv
│       ├── correlation_spearman_portuguese.csv
│       └── correlation_tests_pooled.csv
├── notebooks/
│   └── FIP_B6_analysis.ipynb         # executed notebook
├── charts/
│   ├── 01_grade_distributions.png
│   ├── 02_attendance_patterns.png
│   ├── 03_study_habits_grades.png
│   ├── 04_sampling_comparison.png
│   ├── 05_correlation_heatmap.png
│   ├── 06_vector_similarity.png
│   └── 07_projection_g2_g3.png
├── spreadsheet/
│   ├── B6_statistics_crosscheck.xlsx # live Excel formulas + comparison
│   └── crosscheck_results.csv        # 25/25 PASS
├── docs/
│   ├── DATA_DICTIONARY.md
│   ├── INSIGHTS.md
│   ├── CHART_CRITIQUE_GUIDE.md
│   ├── CROSSCHECK.md
│   └── AUDIT_REPORT.md
└── outputs/
    ├── notebook_execution.log
    └── environment_versions.csv
```

## 3. Setup

**Requirements:** Python 3.11+ (built and tested with Python 3.13.17 on Windows 11).
All tools are free and open source.

```powershell
# from the B6 folder
python -m venv .venv
.\.venv\Scripts\Activate.ps1
python -m pip install --upgrade pip
python -m pip install -r requirements.txt
```

On macOS/Linux, replace the activation line with `source .venv/bin/activate`.

`formulas` is used only to recalculate the spreadsheet cross-check in the notebook.
Excel or LibreOffice is **not** required, though the workbook opens in either and its
formulas recalculate on open.

## 4. Run the notebook

Interactive:

```powershell
jupyter lab
# open notebooks/FIP_B6_analysis.ipynb and choose Kernel > Restart & Run All
```

Command line (reproduces the committed execution and rewrites the outputs):

```powershell
jupyter nbconvert --to notebook --execute --inplace ^
  --ExecutePreprocessor.timeout=900 ^
  --ExecutePreprocessor.kernel_name=python3 ^
  notebooks/FIP_B6_analysis.ipynb
```

The notebook resolves the project root whether the working directory is `B6/` or
`B6/notebooks/`. It verifies the SHA-256 checksums of both raw CSV files before
analysis, so a modified raw file stops the run.

**Expected run time:** about 1–2 minutes on a normal laptop. The slow steps are the two
2,000-resample bootstrap loops, the 1,044 × 1,044 similarity matrix, and the
recalculation of the spreadsheet formulas.

## 5. Data source and licence

- **Kaggle dataset:** *Student Alcohol Consumption*, owner UCI Machine Learning,
  uploaded by Dmitrii Batogov (version 2, last updated 2016-10-19 according to the
  Kaggle API metadata).
  <https://www.kaggle.com/datasets/uciml/student-alcohol-consumption>
- **Download used:** `https://www.kaggle.com/api/v1/datasets/download/uciml/student-alcohol-consumption`
- **Upstream:** UCI Machine Learning Repository, *Student Performance* (ID 320),
  <https://archive.ics.uci.edu/dataset/320/student+performance>,
  DOI <https://doi.org/10.24432/C5TG7T>.
- **Licence:** the Kaggle mirror is labelled **CC0: Public Domain**; the upstream UCI
  record states **CC BY 4.0**. Attribution to Paulo Cortez and António M. G. Silva is
  retained. Full provenance and checksums are in `data/raw/SOURCE.md`.

**Citation:** Cortez, P., & Silva, A. (2008). Using data mining to predict secondary
school student performance. In *Proceedings of the 5th FUBUTEC Conference* (pp. 5–12),
Porto, Portugal. EUROSIS. ISBN 978-9077381-39-7.

## 6. Methods at a glance

- **Descriptive statistics:** n, mean, median, sample SD, quartiles, IQR, skewness,
  kurtosis, pass rates, zero-absence rates, by cohort.
- **Distribution analysis:** histograms with density guides and ECDFs; explicit note
  that grades are discrete and bounded.
- **Attendance:** zero-inflation, band means with 95% confidence intervals,
  Pearson/Spearman correlations, bootstrap intervals.
- **Study habits:** ordinal study-time bands and top-coded failures, Kruskal–Wallis
  tests, Spearman correlations, paid-class comparisons with Mann–Whitney tests and
  Cohen's d.
- **Sampling:** composition tables, chi-square test for sex composition, Welch and
  Mann–Whitney comparisons, school-stratified grade means, and a replication of the
  original R merge to quantify overlap.
- **Correlation:** separate Pearson and Spearman matrices per cohort, Benjamini–Hochberg
  correction across 11 pooled tests, bootstrap confidence intervals, and an explicit
  correlation-versus-causation discussion.
- **Linear algebra:** student feature vectors, dot products, norms, cosine similarity,
  the matrix `X` (1,044 × 5), the Gram matrix `ZᵀZ/(n−1)` as a correlation matrix,
  singular values, rank, condition number, and least-squares projection with
  `R² = cos²θ`.
- **Spreadsheet cross-check:** live formulas for counts, means, medians, sample SDs,
  quartiles, pass rates, Pearson correlations, study-band means and a worked cosine
  similarity; recalculated with the free `formulas` engine and compared to Python.

## 7. Cleaning and data quality

- **Missing values:** 0 cells (1,044 rows × 35 columns after adding `student_id` and
  `subject`).
- **Exact duplicates:** 0 rows.
- **Impossible values:** none; grades 0–20, absences ≥ 0, studytime 1–4.
- **Outlier:** mathematics absences reach 75; the row is retained and flagged
  (`absences_gt30`), not winsorised or deleted.
- **Top-coding:** `failures = 3` means "3 or more"; treated as ordinal.
- **No rows deleted, no imputation applied.** The full decision log is
  `data/processed/cleaning_decisions.csv`.

## 8. Charts

| File | What it shows |
|---|---|
| `01_grade_distributions.png` | Histogram/density and ECDF of G3 by cohort; level, spread and lower tail. |
| `02_attendance_patterns.png` | Zero-inflated absences and band means with 95% CIs; the weak, non-monotonic grade–absence pattern. |
| `03_study_habits_grades.png` | Mean G3 by study-time band and by past failures, with 95% CIs. |
| `04_sampling_comparison.png` | Cohort composition (school, paid classes, sex, internet, etc.) and grade means by subject × school. |
| `05_correlation_heatmap.png` | Spearman correlation matrices for Mathematics and Portuguese. |
| `06_vector_similarity.png` | Cosine-similarity heatmap for 60 students and mean similarity by grade distance. |
| `07_projection_g2_g3.png` | G3 vs G2 scatter with least-squares projection; `r`, `R²` and angle annotation. |

Every chart has a title, a subtitle explaining the encoding/sample, labelled axes with
units, a source note, and a colourblind-safe two-colour palette. Charts are discussed
and critiqued in the notebook and in `docs/CHART_CRITIQUE_GUIDE.md`.

## 9. Key findings (full evidence in `docs/INSIGHTS.md`)

1. **Cohorts differ in level and spread.** Mathematics mean G3 = 10.42 (SD 4.58) vs
   Portuguese 11.91 (SD 3.23); 9.6% vs 2.3% scored 0; 67.1% vs 84.6% reached the pass
   mark.
2. **Attendance is weakly related to grades, and not monotonically.** r = +0.034
   (mathematics, p = 0.497), −0.091 (Portuguese, p = 0.020), pooled −0.046 (95% CI
   −0.103 to +0.009). Mathematics students with zero absences average 8.44, below the
   11.96 of those with 1–2 absences.
3. **Study time matters more in Portuguese; past failures matter in both.** Spearman
   ρ = 0.105 (mathematics) vs 0.275 (Portuguese); failures ρ = −0.361 and −0.448.
4. **The cohorts are different samples.** MS school share 11.6% vs 34.8%; paid classes
   45.8% vs 6.0%. Within GP the grade gap is 2.09 points, within MS 0.80; the raw gap
   is 1.49. The original merge yields 382 rows but only 187 distinct mathematics grade
   triples, so this is not a paired panel.
5. **Prior grade dominates, and correlation is not causation.** G2–G3 r = 0.905/0.919
   (R² = 0.819/0.844); adding absences, study time and failures raises R² only to
   0.826/0.847. Paid tuition shows no significant raw advantage, but uptake is heavily
   selected.

## 10. Spreadsheet cross-check

Open `spreadsheet/B6_statistics_crosscheck.xlsx`:

- `README` — purpose and sheet guide.
- `Math_Data`, `Por_Data` — analysis columns with student IDs.
- `Summary` — COUNT/AVERAGE/MEDIAN/STDEV/QUARTILE.INC/COUNTIF formulas.
- `Correlations` — CORREL formulas.
- `Group_Means` — COUNTIF/AVERAGEIF formulas.
- `Similarity` — worked SUMPRODUCT/SUMSQ cosine example (raw and centred).
- `Comparison` — spreadsheet value vs Python value, absolute difference, PASS/CHECK.

The notebook recalculates the workbook with `formulas` 1.3.4 and requires agreement
within 1 × 10⁻⁹. Result: **25/25 checks PASS**, maximum absolute difference
**1.22 × 10⁻¹⁵** (floating-point noise). The same table is in
`spreadsheet/crosscheck_results.csv` and `docs/CROSSCHECK.md`.

## 11. Limitations

- **Observational data.** No random assignment, no control group; causal claims about
  attendance, study time or tutoring are not supported.
- **Convenience sample.** Two Portuguese schools, not a random or national sample;
  results may not generalise. The two subject cohorts differ in composition.
- **Non-independent overlap.** 382 approximate matches between files; many-to-many, so
  the pooled 1,044 rows overstate the effective independent sample size.
- **Measurement limits.** Discrete bounded grades, coarse self-reported study time,
  top-coded failures, school-record absences, and unmeasured confounders.
- **Small subgroups.** Some study-time/failure cells contain 14–35 students and have
  wide confidence intervals.
- **Multiple testing.** Addressed with Benjamini–Hochberg for the 11 pooled correlations
  with G3, but the project remains exploratory.

## 12. Troubleshooting

| Problem | Fix |
|---|---|
| `ModuleNotFoundError` | Activate the virtual environment and run `pip install -r requirements.txt`. |
| Jupyter kernel not found | `python -m ipykernel install --user --name b6-venv --display-name "Python (B6 venv)"`, then select that kernel. |
| `Raw data not found` | Run Jupyter from the `B6/` or `B6/notebooks/` folder; the notebook resolves both. Do not move the CSV files. |
| Checksum assertion fails | The raw files were edited. Restore the original Kaggle archive; expected hashes are in `data/raw/SOURCE.md`. |
| `formulas` recalculation is slow | It is a pure-Python engine; expect 10–30 seconds. Excel/LibreOffice can open the workbook instead. |
| Charts show missing glyphs | The notebook uses DejaVu Sans, bundled with Matplotlib. |

## 13. Reproducibility notes

- Random seed: `20261113`; bootstrap resamples: 2,000.
- Raw-file SHA-256 checks are enforced at the start of the notebook.
- All derived tables and figures are regenerated by Run All; no manual editing.
- Environment versions used for the committed run are in
  `outputs/environment_versions.csv`.
- The notebook was last executed with `nbconvert` (see
  `outputs/notebook_execution.log`).

## 14. Academic integrity and scope

This is an independent B6 build. It does not modify B4 or B5 and does not start B7.
The project is published in a public GitHub repository:
<https://github.com/fatimamuhammadbashir/b6-statistics-linear-algebra-visualization>.
The FIP assignment submission is still pending.
