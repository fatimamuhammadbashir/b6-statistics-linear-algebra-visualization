# Data source and provenance

## Primary source (Kaggle)

- **Dataset:** *Student Alcohol Consumption*
- **Kaggle owner:** UCI Machine Learning (uploaded by Dmitrii Batogov)
- **Kaggle URL:** https://www.kaggle.com/datasets/uciml/student-alcohol-consumption
- **Kaggle API download used:** `https://www.kaggle.com/api/v1/datasets/download/uciml/student-alcohol-consumption`
- **Kaggle version:** 2 (last updated 2016-10-19 according to the Kaggle API metadata)
- **Kaggle licence label:** CC0: Public Domain
- **Downloaded:** 2026-11-13
- **Files in the archive:** `student-mat.csv`, `student-por.csv`, `student-merge.R`

## Original study and upstream repository

The Kaggle dataset is a mirror of the UCI Machine Learning Repository dataset
*Student Performance* (ID 320):

- **UCI page:** https://archive.ics.uci.edu/dataset/320/student+performance
- **DOI:** https://doi.org/10.24432/C5TG7T
- **Original licence (UCI):** Creative Commons Attribution 4.0 International (CC BY 4.0)
- **Creators:** Paulo Cortez, António M. G. Silva (University of Minho)
- **Citation:** Cortez, P., & Silva, A. (2008). Using data mining to predict secondary
  school student performance. In *Proceedings of the 5th FUBUTEC Conference*
  (pp. 5–12). EUROSIS. ISBN 978-9077381-39-7.

Because the upstream UCI licence is CC BY 4.0, attribution to Cortez and Silva is
retained here even though the Kaggle mirror is labelled CC0.

## File checksums (SHA-256)

| File | SHA-256 |
|---|---|
| `student-mat.csv` | `659F3984643C2DEF53BA5E49F551C6CE3657039F9C25306CACB8F43B818A5190` |
| `student-por.csv` | `3FB408FE4B66D4CDB90AD4EC5E3FB6DE94BA662D0471A3D46C03DA483069F76B` |

Checksums were computed on the files exactly as extracted from the Kaggle archive.
The raw CSV files are stored unmodified.

## What the data contains

Two separate cohorts of secondary-school students in Portugal:

| File | Subject | Rows | Columns |
|---|---|---:|---:|
| `student-mat.csv` | Mathematics | 395 | 33 |
| `student-por.csv` | Portuguese language | 649 | 33 |

Columns cover demographics, family background, school support, study habits,
free time, alcohol consumption, health, absences, and three period grades
(G1, G2, G3) on a 0–20 scale. According to the dataset documentation, 382 students
appear in both cohorts; they can be matched on the shared background attributes
(see `student-merge.R`, reproduced from the original archive).

## Important caveats

- The data are **observational**, from two Portuguese secondary schools, collected
  via school reports and questionnaires. They are not a random sample of any
  national or international population.
- `G3` is the final grade and is strongly related to `G1` and `G2` by construction
  (same course, successive assessment periods). Correlations involving grades are
  partly mechanical.
- `absences` counts reported school absences; it is a proxy for attendance, not a
  direct measure of attendance in every class.
- `studytime` is a coarse self-reported ordinal band (1 = <2 h/week, 2 = 2–5 h,
  3 = 5–10 h, 4 = >10 h), not a continuous number of hours.
- The Kaggle mirror is used as the assignment's Kaggle source; the original UCI
  dataset and paper are cited for scientific context.
