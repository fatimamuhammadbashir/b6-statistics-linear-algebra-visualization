# Data dictionary

The dataset has 33 source columns per cohort plus two columns added by this project
(`student_id` and `subject`). Definitions below follow the Kaggle dataset card and the
UCI *Student Performance* documentation (Cortez & Silva, 2008).

## Identifiers added by this project

| Column | Type | Description |
|---|---|---|
| `student_id` | string | Row label constructed for traceability: `MAT-001`…`MAT-395`, `POR-001`…`POR-649`. Not a real person identifier. |
| `subject` | category | `Mathematics` or `Portuguese`, derived from the source file. |

## Source variables (both files)

| # | Column | Type | Values / units | Notes |
|---:|---|---|---|---|
| 1 | `school` | categorical | `GP` = Gabriel Pereira; `MS` = Mousinho da Silveira | Two Portuguese secondary schools. |
| 2 | `sex` | categorical | `F`, `M` | Binary recorded sex. |
| 3 | `age` | integer | 15–22 years | Age at the time of the survey. |
| 4 | `address` | categorical | `U` = urban, `R` = rural | Home address type. |
| 5 | `famsize` | categorical | `LE3` = ≤3, `GT3` = >3 | Family size. |
| 6 | `Pstatus` | categorical | `T` = living together, `A` = apart | Parents' cohabitation status. |
| 7 | `Medu` | ordinal | 0–4 | Mother's education: 0 none, 1 primary, 2 lower secondary, 3 secondary, 4 higher. |
| 8 | `Fedu` | ordinal | 0–4 | Father's education, same scale as `Medu`. |
| 9 | `Mjob` | categorical | `teacher`, `health`, `services`, `at_home`, `other` | Mother's occupation. |
| 10 | `Fjob` | categorical | `teacher`, `health`, `services`, `at_home`, `other` | Father's occupation. |
| 11 | `reason` | categorical | `home`, `reputation`, `course`, `other` | Reason for choosing the school. |
| 12 | `guardian` | categorical | `mother`, `father`, `other` | Student's guardian. |
| 13 | `traveltime` | ordinal | 1–4 | Home-to-school travel time: 1 <15 min, 2 15–30 min, 3 30–60 min, 4 >1 h. |
| 14 | `studytime` | ordinal | 1–4 | Weekly study time: 1 <2 h, 2 2–5 h, 3 5–10 h, 4 >10 h. Coarse self-report. |
| 15 | `failures` | ordinal / count | 0–3 | Number of past class failures; **3 means 3 or more**. Top-coded. |
| 16 | `schoolsup` | binary | `yes`, `no` | Extra educational support from the school. |
| 17 | `famsup` | binary | `yes`, `no` | Family educational support. |
| 18 | `paid` | binary | `yes`, `no` | Extra paid classes in the course subject. |
| 19 | `activities` | binary | `yes`, `no` | Extra-curricular activities. |
| 20 | `nursery` | binary | `yes`, `no` | Attended nursery school. |
| 21 | `higher` | binary | `yes`, `no` | Wants to take higher education. |
| 22 | `internet` | binary | `yes`, `no` | Internet access at home. |
| 23 | `romantic` | binary | `yes`, `no` | In a romantic relationship. |
| 24 | `famrel` | ordinal | 1–5 | Quality of family relationships: 1 very bad … 5 excellent. |
| 25 | `freetime` | ordinal | 1–5 | Free time after school: 1 very low … 5 very high. |
| 26 | `goout` | ordinal | 1–5 | Going out with friends: 1 very low … 5 very high. |
| 27 | `Dalc` | ordinal | 1–5 | Workday alcohol consumption: 1 very low … 5 very high. |
| 28 | `Walc` | ordinal | 1–5 | Weekend alcohol consumption: 1 very low … 5 very high. |
| 29 | `health` | ordinal | 1–5 | Current health status: 1 very bad … 5 very good. |
| 30 | `absences` | count | 0–93 documented; observed 0–75 (math), 0–32 (por) | Number of school absences. Proxy for attendance, not class-specific. |
| 31 | `G1` | grade | 0–20 | First-period grade in the subject. |
| 32 | `G2` | grade | 0–20 | Second-period grade in the subject. |
| 33 | `G3` | grade | 0–20 | Final grade in the subject (target variable). |

## Derived variable created in the notebook

| Column | Type | Description |
|---|---|---|
| `absences_gt30` | binary | 1 if `absences > 30`, else 0. Used only as a sensitivity flag; no rows are removed. |

## Analysis conventions

- Pass mark: `G3 >= 10` on the Portuguese 0–20 scale.
- Cohorts are kept separate for inference. Pooled statistics always show the cohort
  composition and are described as descriptive.
- `studytime` and `failures` are treated as ordinal; equal spacing is **not** assumed in
  the statistical tests (Spearman / Kruskal–Wallis). Charts place them on evenly spaced
  positions for readability only.
- Missing values: none. No imputation was applied.
