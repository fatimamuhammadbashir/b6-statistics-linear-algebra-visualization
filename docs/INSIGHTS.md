# Five data-supported insights

All numbers below are computed from `data/raw/student-mat.csv` and
`data/raw/student-por.csv` by `notebooks/FIP_B6_analysis.ipynb`. They are rounded for
readability; the unrounded values are in `data/processed/` and in the notebook outputs.

---

## Insight 1 — Final grades differ by cohort in level, spread and lower tail

| Evidence | Mathematics | Portuguese |
|---|---:|---:|
| n | 395 | 649 |
| Mean G3 (0–20) | 10.42 | 11.91 |
| SD G3 | 4.58 | 3.23 |
| Median G3 | 11 | 12 |
| IQR | 6 | 4 |
| Scored 0 | 9.6% | 2.3% |
| Reached pass mark (G3 ≥ 10) | 67.1% | 84.6% |

**Interpretation.** The Portuguese cohort sits about 1.49 points higher on average and
is much more tightly clustered. The mathematics distribution is flatter and has a
pronounced spike at zero, so its lower average is driven by a heavier lower tail rather
than by a modest shift of the whole distribution.

**Why it matters.** An average grade quoted without its cohort mixes two different
distributions. The ECDF in Figure 1 shows that the gap is largest in the lower half of
the grade range.

**Caveat.** This is a descriptive difference between two subject cohorts, not proof
that one subject is graded more harshly. School composition and selection differ
between cohorts (Insight 4).

---

## Insight 2 — Attendance is only weakly related to grades, and not monotonically

| Evidence | Mathematics | Portuguese |
|---|---:|---:|
| Pearson r (absences, G3) | +0.034 | −0.091 |
| p-value | 0.497 | 0.020 |
| Spearman ρ | +0.018 | −0.159 |
| Mean G3 at 0 absences | 8.44 | 12.04 |
| Mean G3 at 1–2 absences | 11.96 | 12.21 |
| Mean G3 at 11–20 absences | 10.12 | 10.63 |
| Mean G3 at 21+ absences | 10.27 | 10.75 |

Pooled across cohorts: r = −0.046 (p = 0.140), bootstrap 95% CI −0.103 to +0.009.

**Interpretation.** The association is weak in both cohorts and not monotonic. In
mathematics, the zero-absence group has the *lowest* mean grade, which is the opposite
of a simple “attendance protects grades” story. In Portuguese the decline is smoother
but still modest: even r = −0.091 implies less than 1% of grade variance.

**Why it matters.** “More absences cause lower grades” is not supported by a simple
correlation in these data. The zero-absence group may differ in prior attainment,
health, family circumstances or school rules, and low grades can themselves cause
disengagement and absence.

**Caveat.** `absences` is a school-record proxy, not class-specific attendance. The
math distribution has a 75-absence outlier; the Portuguese tail reaches 32.

---

## Insight 3 — Study time tracks grades more clearly in Portuguese; past failures track them in both

| Evidence | Mathematics | Portuguese |
|---|---:|---:|
| Mean G3, studytime 1 (<2 h) | 10.05 | 10.84 |
| Mean G3, studytime 2 (2–5 h) | 10.17 | 12.09 |
| Mean G3, studytime 3 (5–10 h) | 11.40 | 13.23 |
| Mean G3, studytime 4 (>10 h) | 11.26 | 13.06 |
| Spearman ρ (studytime, G3) | 0.105 | 0.275 |
| p-value | 0.037 | < 0.001 |
| Kruskal–Wallis p | 0.056 | < 0.001 |
| Mean G3, 0 failures | 11.25 | 12.51 |
| Mean G3, 3+ failures | 5.69 | 8.07 |
| Spearman ρ (failures, G3) | −0.361 | −0.448 |

**Interpretation.** The Portuguese study-time gradient is clear and monotonic up to the
5–10 h band; the mathematics gradient is weak and the top band (n = 27) is imprecise.
Past failures show a stronger and more consistent negative gradient in both cohorts:
students with three or more failures average roughly 5–6 points below students with
none.

**Why it matters.** The behavioural signal is real but context-dependent. Prior failure
is a stronger marker of final grade than self-reported study time, which may reflect
that failures capture accumulated academic difficulty rather than effort alone.

**Caveat.** `studytime` is a coarse ordinal self-report (four bands), and `failures` is
top-coded at 3 and is a prior-attainment proxy. Neither is a causal lever. Students who
struggle may report more study time, creating reverse causality.

---

## Insight 4 — The two cohorts are different samples, so the raw gap is not a subject effect

| Evidence | Mathematics | Portuguese |
|---|---:|---:|
| Attends MS school | 11.6% | 34.8% |
| Paid classes | 45.8% | 6.0% |
| Female | 52.7% | 59.0% |
| Rural address | 22.3% | 30.4% |
| Wants higher education | 94.9% | 89.4% |
| Mean G3 within GP school | 10.49 (n = 349) | 12.58 (n = 423) |
| Mean G3 within MS school | 9.85 (n = 46) | 10.65 (n = 226) |

Raw mean difference: 1.49 points (Portuguese higher). Within GP: 2.09 points. Within
MS: 0.80 points. Sex composition chi-square: p = 0.052.

**Interpretation.** School composition is entangled with subject cohort. The Portuguese
cohort has three times the share of MS students, and MS students score lower on
average. Standardising both cohorts to the same school mix raises the gap from 1.49 to
about 1.75 points. The raw 1.49-point gap therefore cannot be read as
“Portuguese is easier” or “Portuguese students are better”; it is a mix of subject,
school, intake and selection.

**Overlap caveat.** Applying the matching keys from the original `student-merge.R`
produces 382 matched rows, but the merge is many-to-many: those rows contain only 187
distinct mathematics grade triples. The matched mathematics and Portuguese grades
correlate at 0.48 and absences at 0.50. The files are not a clean paired panel, so
pooling all 1,044 rows as independent observations overstates the effective sample
size.

---

## Insight 5 — Prior grade dominates, and correlation does not establish causation

| Evidence | Mathematics | Portuguese |
|---|---:|---:|
| Pearson r (G2, G3) | 0.905 | 0.919 |
| R² (G2 alone) | 0.819 | 0.844 |
| R² (G2 + absences + studytime + failures) | 0.826 | 0.847 |
| Standardised β for studytime | −0.03 | +0.03 |
| Mean G3 with paid classes | 10.92 | 11.21 |
| Mean G3 without paid classes | 9.99 | 11.95 |
| Mann–Whitney p for paid classes | 0.227 | 0.149 |

**Interpretation.** The previous grade in the same course explains 82–84% of the
variance in the final grade. Adding absences, study time and failures raises R² by less
than one percentage point, and the standardised study-time coefficient is essentially
zero. Paid tuition shows no significant raw advantage, but uptake is heavily selected
(45.8% in mathematics vs 6.0% in Portuguese), so this is not evidence about tutoring's
effect.

**Why correlation is not causation here.** (1) G1–G3 are successive assessments of the
same course, so their correlation is partly mechanical. (2) Prior attainment, motivation
and family resources confound the behavioural correlations. (3) Students select into
paid tuition, subjects and schools. (4) Low grades can cause disengagement and absence,
not only the reverse. (5) Eleven correlations with G3 were tested; after
Benjamini–Hochberg correction, absences is not significant (q = 0.14), while studytime
and failures remain so. (6) Absences are zero-inflated with a long tail, so a single
Pearson coefficient cannot capture the shape.

**Caveat.** A non-significant raw difference is not evidence that tutoring is
ineffective. It means these observational data cannot isolate the effect.

---

## Overall conclusion

The dataset is well suited to describing this student population and to practising
statistical and linear-algebra reasoning. It is not a basis for causal claims about
attendance, study time or tutoring, and it is not a random sample of students beyond
these two Portuguese schools. The strongest, most stable pattern is the association
between successive grades in the same subject — which is also the least causal-looking
pattern in the data.
