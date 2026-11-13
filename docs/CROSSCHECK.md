# Spreadsheet cross-check

This document records the spreadsheet cross-check required by the B6 brief. Selected statistics are recomputed with **live spreadsheet formulas** in `spreadsheet/B6_statistics_crosscheck.xlsx` and compared with the independent Python/pandas values produced by the notebook.

## Workbook structure

| Sheet | Contents |
|---|---|
| `README` | Purpose, source and sheet guide. |
| `Math_Data` | 395 mathematics rows: `student_id`, G1, G2, G3, absences, studytime, failures. |
| `Por_Data` | 649 Portuguese rows, same columns. |
| `Summary` | Count, mean, median, sample SD, min, Q1, Q3, max, pass rate and zero-absence share, with live formulas. |
| `Correlations` | Pearson correlations with G3 (`CORREL`). |
| `Group_Means` | Mean G3 by study-time band (`COUNTIF` / `AVERAGEIF`). |
| `Similarity` | Worked cosine similarity for MAT-001 vs MAT-019 (`SUMPRODUCT`, `SUMSQ`, `SQRT`), raw and centred. |
| `Comparison` | Spreadsheet value, Python value, absolute difference and PASS/CHECK status. |

## Selected calculations checked

- Sample counts, means, medians, sample standard deviations and pass rates for G3, by cohort.
- Pearson correlations of G3 with G2 and with absences, by cohort.
- Mean G3 for each of the four study-time bands, by cohort.
- Worked cosine similarity (raw and centred) and Euclidean distance for two named students.

## Method

The workbook is written by the notebook with openpyxl. Every checked value is a live formula, not a pasted number. The notebook then recalculates the workbook with the free `formulas` engine (version 1.3.4) and compares each formula result with the value computed independently in pandas/NumPy. The tolerance is 1 × 10⁻⁹. Excel or LibreOffice will recalculate the same formulas on open; `formulas` is used here so the check is reproducible without proprietary software.

## Results

| Check | Spreadsheet | Python | Absolute difference | Status |
|---|---:|---:|---:|:---:|
| Mathematics: n | 395 | 395 | 0.00e+00 | PASS |
| Mathematics: mean G3 | 10.4151898734 | 10.4151898734 | 0.00e+00 | PASS |
| Mathematics: median G3 | 11 | 11 | 0.00e+00 | PASS |
| Mathematics: SD G3 | 4.581442611 | 4.581442611 | 0.00e+00 | PASS |
| Mathematics: % G3 >= 10 | 0.670886075949 | 0.670886075949 | 0.00e+00 | PASS |
| Portuguese: n | 649 | 649 | 0.00e+00 | PASS |
| Portuguese: mean G3 | 11.906009245 | 11.906009245 | 0.00e+00 | PASS |
| Portuguese: median G3 | 12 | 12 | 0.00e+00 | PASS |
| Portuguese: SD G3 | 3.2306562428 | 3.2306562428 | 0.00e+00 | PASS |
| Portuguese: % G3 >= 10 | 0.845916795069 | 0.845916795069 | 0.00e+00 | PASS |
| Mathematics: r(G3,G2) | 0.904867989269 | 0.904867989269 | 1.11e-15 | PASS |
| Mathematics: r(G3,absences) | 0.0342473161501 | 0.0342473161501 | 9.02e-17 | PASS |
| Portuguese: r(G3,G2) | 0.91854800356 | 0.91854800356 | 1.22e-15 | PASS |
| Portuguese: r(G3,absences) | -0.0913790564388 | -0.0913790564388 | 2.22e-16 | PASS |
| Mathematics: studytime 1 mean | 10.0476190476 | 10.0476190476 | 0.00e+00 | PASS |
| Mathematics: studytime 2 mean | 10.1717171717 | 10.1717171717 | 0.00e+00 | PASS |
| Mathematics: studytime 3 mean | 11.4 | 11.4 | 0.00e+00 | PASS |
| Mathematics: studytime 4 mean | 11.2592592593 | 11.2592592593 | 0.00e+00 | PASS |
| Portuguese: studytime 1 mean | 10.8443396226 | 10.8443396226 | 0.00e+00 | PASS |
| Portuguese: studytime 2 mean | 12.0918032787 | 12.0918032787 | 0.00e+00 | PASS |
| Portuguese: studytime 3 mean | 13.2268041237 | 13.2268041237 | 0.00e+00 | PASS |
| Portuguese: studytime 4 mean | 13.0571428571 | 13.0571428571 | 0.00e+00 | PASS |
| MAT-001 vs MAT-019: raw cosine | 0.867262375282 | 0.867262375282 | 0.00e+00 | PASS |
| MAT-001 vs MAT-019: centred cosine | 0.593382929805 | 0.593382929805 | 0.00e+00 | PASS |
| MAT-001 vs MAT-019: Euclidean distance | 10.1980390272 | 10.1980390272 | 0.00e+00 | PASS |

**Summary:** 25/25 checks PASS; maximum absolute difference = **1.22e-15**. The residual differences are floating-point noise, not disagreements about the statistics.

## How to reproduce in Excel or LibreOffice

1. Open `spreadsheet/B6_statistics_crosscheck.xlsx`.
2. Allow formulas to recalculate (Excel does this on open; LibreOffice may ask).
3. Inspect `Comparison`; column E should read PASS for every row.
4. To re-run the automated check, execute the notebook from top to bottom; it rewrites the workbook and `crosscheck_results.csv`.

## What the check does and does not cover

The check validates the arithmetic pipeline for a representative set of statistics: counts, location, spread, pass rates, correlations, group means and a vector similarity example. It does **not** re-derive every number in the notebook, and it does not validate the modelling assumptions or the causal interpretation. Those are discussed in the notebook and in `docs/INSIGHTS.md`.
