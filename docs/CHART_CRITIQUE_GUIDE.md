# Chart Critique Guide

A practical guide for judging whether a chart communicates data honestly, clearly and
usefully. It is written for the B6 project but applies to any exploratory data
visualisation. The last section reviews the seven charts in this project against the
same criteria.

---

## 1. The five-question test

Before judging a chart, answer these five questions in order.

1. **What question is the chart answering?** A chart should have a purpose that can be
   stated in one sentence. If the title only names the variables ("G3 by studytime"),
   the purpose is not yet clear.
2. **What is encoded, and on what scale?** Identify the mark (bar, point, line, area),
   the channels (position, length, colour, angle) and the units. Position and length are
   read accurately; angle and area are not.
3. **What claim does the chart appear to make?** Read the title, subtitle, axis labels
   and annotations as a single argument. A chart can imply causality or a trend even
   when the underlying statistic does not support it.
4. **What could mislead a careful reader?** Check the axis, binning, aggregation,
   sample size, uncertainty, colour and selection of cases.
5. **What would make the chart more honest or more useful?** Usually one of: show the
   distribution instead of only the mean, add a denominator, add uncertainty, annotate
   n, simplify the encoding.

A chart that survives all five questions is not necessarily beautiful, but it is
defensible.

---

## 2. Choosing the right chart

| Question | Suitable chart | Avoid |
|---|---|---|
| Distribution of one variable | Histogram, ECDF, box plot, violin plot | Pie chart, single average |
| Distribution across groups | Grouped histograms, box plots, strip/jitter plots, ECDFs | 3-D bars, overlapping pies |
| Comparison of group means | Dot plot with confidence intervals, bar chart with error bars (if n is shown) | Bar chart with truncated axis |
| Relationship between two variables | Scatter plot, hexbin, binned means with intervals | Two bars side by side, correlation heatmap alone |
| Trend over an ordered variable | Line with points, ECDF, heatmap for matrices | Rainbow colour for a single trend |
| Composition | Stacked bar (few categories), 100% stacked bar, dot plot | Pie chart with many slices, 3-D pie |
| Correlation matrix | Heatmap with a diverging palette, annotated values, masked redundancy | Rainbow palette, unlabelled 20 × 20 grid |
| Part-to-whole over time | Stacked area (with caution), small multiples | Dual axes, overlapping areas |

**Rule of thumb:** if the reader's main task is to compare values, use position or
length. If the main task is to see a distribution, show the distribution — not only a
summary.

---

## 3. Integrity checks

### Axes and baselines

- **Bar charts must start at zero.** Bars encode magnitude by length; a truncated
  baseline exaggerates differences. If zero is impossible (e.g. log scale), label the
  scale explicitly.
- **Line charts and dot plots may use a non-zero baseline** when the question is about
  change rather than magnitude — but the axis must be labelled and the choice explained.
- **Do not break an axis** without a clear visual marker and a note.
- **Keep aspect ratio honest.** Stretching a chart vertically can turn a small
  difference into a dramatic slope.

### Aggregation

- A mean is not a distribution. Show spread (SD, IQR, confidence interval) or the raw
  points whenever decisions depend on variability.
- State the denominator. "70% passed" means nothing without "of whom".
- Beware of **Simpson's paradox**: an association can reverse when groups are combined.
  In B6, the grade gap between cohorts changes when school composition is considered.
- Check that group sizes are visible. A mean based on 14 students should not look as
  authoritative as one based on 600.

### Uncertainty

- Show confidence intervals or standard errors when comparing group means.
- For proportions, show the numerator and denominator or a confidence interval.
- Do not use significance stars as a substitute for effect size.
- Distinguish **statistical significance** (compatible with a non-zero effect) from
  **practical importance** (size and consequences).

### Binning

- Histogram conclusions can depend on bin width and origin. Try at least one
  alternative before making a strong claim.
- For discrete data (grades 0–20), use integer-aligned bins and say so.
- Binned means can create the appearance of a trend; show the bin edges and the n per
  bin.

### Colour

- Use a **colourblind-safe** palette. B6 uses blue (#0072B2) for Mathematics and
  vermillion (#D55E00) for Portuguese, from the Okabe–Ito palette.
- Use **sequential** palettes for ordered magnitude, **diverging** palettes for
  correlation or signed change (centred at zero), and **qualitative** palettes for
  unordered categories. Do not use a rainbow for ordered data.
- Never encode the same variable twice (e.g. bar height and colour) unless it aids
  grouping; redundant encoding is acceptable only when it does not imply extra meaning.
- Check contrast in greyscale and for deuteranopia/protanopia.

### Labels and context

A publishable chart needs:

- a **title that states the takeaway**, not just the variables;
- a **subtitle** defining the sample, metric, time period and units;
- **axis labels with units** (e.g. "Final grade G3 (0–20)", not "score");
- **direct labels** where possible, so the reader does not have to decode a legend;
- **n** for each group or an explicit note;
- a **source note**, including the dataset and any exclusions;
- a note on **transformations** (log scale, standardisation, smoothing, jitter).

### Selection and exclusions

- State what was excluded and why. In B6, absences above 25 are omitted from the
  histogram panel but counted in the legend; the band means use all rows.
- Do not silently drop outliers. Show them, cap them with a note, or report a
  sensitivity analysis.
- A chart of "top 10" or "selected schools" is a selection claim, not a population
  claim.

---

## 4. Statistical honesty

### Correlation is not causation

A scatter plot or heatmap shows co-variation. It does not identify direction,
mechanism, or a counterfactual. Before writing causal language, ask:

- **Reverse causality:** could Y cause X? (Low grades → disengagement → absence.)
- **Confounding:** is a third variable driving both? (Prior attainment, family
  resources, school quality.)
- **Selection:** who is in the sample, and why? (Paid tuition, subject choice, school.)
- **Mechanical dependence:** are the variables constructed from one another? (G1, G2,
  G3 are successive grades in the same course.)
- **Chance:** how many comparisons were made? (Eleven correlations with G3 in B6.)
- **Non-linearity:** would a single coefficient misrepresent the shape? (Zero-inflated
  absences.)

Use associational verbs — "is associated with", "co-varies with", "differs by" — unless
the design supports something stronger.

### Effect size before p-value

Report the size of the difference or association (mean difference, Cohen's d, r, R²,
risk ratio) and its uncertainty. A p-value answers a narrow question about compatibility
with a null model; it does not measure importance.

### Multiple comparisons

If many tests are run, say so and correct or pre-specify. B6 reports Benjamini–Hochberg
q-values for the 11 pooled correlations with G3 and notes that absences does not survive
correction.

### Missing data

State the amount and pattern of missingness, the handling method, and the assumption it
requires. "Complete-case analysis" is a decision, not a neutral default. B6 has no
missing values, so no imputation was needed; this is documented rather than assumed.

---

## 5. Accessibility

- Provide **alt text** or a caption that conveys the takeaway for readers who cannot see
  the image.
- Do not rely on colour alone; use direct labels, shapes or line styles.
- Use a minimum font size of about 9 pt in a figure intended for a report; 7–8 pt is
  acceptable only for secondary annotations.
- Avoid clutter: remove gridlines that do not help, redundant legends, and decorative
  backgrounds.
- Make interactive or high-resolution versions available when the static chart
  overplots (B6 exports at 200 dpi).
- Check that the chart still works when printed in greyscale.

---

## 6. Critique template

Copy this form for each chart review.

```text
Chart:
Reviewer:
Date:

1. Question the chart answers:
2. Audience and decision it should support:
3. Marks, channels, units:
4. What the chart claims (title + subtitle + annotation):
5. Data integrity:
   - baseline / axis:
   - aggregation and denominator:
   - uncertainty:
   - binning or smoothing:
   - exclusions:
6. Encoding quality:
   - chart type appropriate?
   - colour appropriate and accessible?
   - overplotting?
7. Labelling:
   - title states takeaway?
   - axes and units?
   - n and source?
8. Statistical honesty:
   - causal language?
   - effect size and uncertainty?
   - multiple comparisons?
9. What works (keep):
10. What could mislead (fix):
11. Recommended revision (one or two concrete changes):
12. Verdict: accept / revise / reject
```

---

## 7. Review of the seven B6 charts

### Figure 1 — Final-grade distributions

**What works.** The histogram shows shape and the zero spike; the ECDF shows the full
distribution without binning and supports direct pass-rate statements. Means are marked
but do not replace the distribution. Both panels share the same x-scale.

**Risks.** A KDE over integer grades can suggest mass between integer values; the
histogram's appearance depends on the 1-point bin width. The pass mark is marked with a
dotted line, but the chart does not show uncertainty around the pass rates.

**Recommended revision.** Keep the ECDF as the primary panel; if a density is retained,
label it "smooth guide only" (as the source note does) or replace it with a probability
mass function.

### Figure 2 — Attendance patterns

**What works.** Panel A makes zero-inflation visible; panel B shows band means with 95%
confidence intervals and uses a shared absence-band definition. The exclusion of
absences above 25 is stated in the subtitle, legend and source note.

**Risks.** Truncating the x-axis hides the extreme tail; band boundaries are
analyst-defined; band means can suggest a trend even when the underlying correlation is
near zero. The 21+ band contains only 15 mathematics and 8 Portuguese students, so its
mean is unstable.

**Recommended revision.** Add a strip or box plot for the raw distribution within bands,
or annotate the n per band directly. Keep the "not monotonic" wording; it is the honest
reading.

### Figure 3 — Study habits and grades

**What works.** Two behaviours are compared on the same scale; confidence intervals and
group sizes are available in the tables; the ordinal nature of the predictors is
acknowledged.

**Risks.** Ordinal bands are placed at equal spacing, which is a visual convenience;
group means hide within-group spread; the top study-time band is small (n = 27
mathematics, 35 Portuguese). The initial version annotated every n and produced
overlapping labels; the final version removes those annotations and points to the table.

**Recommended revision.** Add a small box or violin panel for the distribution, or a
table of n and IQR beneath the figure. Do not connect ordinal categories with a line
without saying the line is a guide.

### Figure 4 — Sampling comparison

**What works.** Panel A makes composition differences concrete; panel B separates the
subject gap by school, which is the key confound. Percentages are explicitly
within-cohort, not population estimates.

**Risks.** Bars can imply population prevalence; the MS mathematics group is small
(n = 46); the panel does not show uncertainty for the composition percentages. The
figure cannot establish why the cohorts differ.

**Recommended revision.** Add binomial confidence intervals to the composition bars, or
show counts alongside percentages. Keep the "not two arms of an experiment" framing.

### Figure 5 — Correlation heatmap

**What works.** Separate cohorts avoid pooling artefacts; Spearman is appropriate for
ordinal/skewed variables; the lower triangle is masked to reduce redundancy; the
diverging palette is centred at zero; the G1–G3 mechanical dependence is flagged.

**Risks.** A 9 × 9 grid with 2-decimal annotations is dense; colour saturation can make
weak correlations look important; significance is not shown; the ordering is arbitrary
and does not cluster related variables.

**Recommended revision.** Cluster variables by similarity, or show only the G3 column as
a dot plot for the main narrative and keep the full matrix as an appendix. Add a note
that the diagonal is 1 by construction.

### Figure 6 — Vector similarity

**What works.** Standardisation is stated; the heatmap is ordered by grade; panel B
quantifies the visual pattern with pair counts; the feature set and the reflection of
absences are documented.

**Risks.** The 60-student sample is selected for display, not random; cosine similarity
depends on the chosen features and scaling; the heatmap has no axis ticks, so individual
students cannot be identified; a diagonal of 1 is meaningless and is excluded from the
statistics.

**Recommended revision.** Add a small inset showing the two worked student vectors, and
state the null baseline (mean similarity ≈ 0) so readers can judge the gradient.

### Figure 7 — Projection / least squares

**What works.** The scatter shows the raw relationship; the fitted line is labelled with
its equation; `r`, `R²` and the angle are annotated; the source note says the line is
descriptive, not causal.

**Risks.** Discrete grades produce overplotting; the line can imply prediction or
causation; the legend occupies space inside the plotting area; the axis limits are
slightly wider than the data.

**Recommended revision.** Add mild transparency/jitter or a count-based hexbin, and put
the equation in the subtitle rather than the legend. Report a confidence band for the
fit if prediction is the goal.

---

## 8. Worked example: the same data, two chart choices

**Poor version:** a bar chart of mean G3 for Mathematics vs Portuguese, y-axis starting
at 9.5, no n, no error bars, title "Portuguese students perform better". This
exaggerates a 1.5-point difference, hides the much larger spread in mathematics, and
implies a causal group ranking.

**Better version:** the ECDF in Figure 1, with n in the legend, a labelled 0–20 axis, a
marked pass mark, and a title that describes the distributional difference rather than
ranking students. The reader can see both the level shift and the heavier lower tail.

**Lesson:** the same statistic can be made to look dramatic or modest by changing the
baseline, the aggregation and the wording. Integrity is mostly about those three
choices.

---

## 9. Red flags checklist

- [ ] Bar chart does not start at zero (and no explanation).
- [ ] Truncated axis used to exaggerate a small difference.
- [ ] Dual y-axes with unrelated units.
- [ ] 3-D chart, exploded pie, or perspective distortion.
- [ ] Rainbow palette applied to an ordered variable.
- [ ] No n, no denominator, no source.
- [ ] Mean-only chart with no spread or uncertainty.
- [ ] Causal language ("causes", "leads to", "improves") from observational data.
- [ ] p-values without effect sizes.
- [ ] Many comparisons without correction or acknowledgement.
- [ ] Cherry-picked time window, subgroup or threshold.
- [ ] Inconsistent colours or group order across panels.
- [ ] Legend requires repeated eye movement; no direct labels.
- [ ] Overplotting hides density or outliers.
- [ ] Title states a conclusion the chart does not support.

---

## 10. Peer-review rubric (100 points)

| Criterion | Points | What full marks looks like |
|---|---:|---|
| Clear question and takeaway | 15 | Title and subtitle state the question and the finding precisely. |
| Appropriate chart type | 15 | Encoding matches the task; distribution shown where needed. |
| Data integrity | 20 | Honest axes, denominators, exclusions and uncertainty. |
| Statistical honesty | 20 | Effect sizes, intervals, no causal overreach, multiple-testing noted. |
| Labelling and context | 15 | Units, n, source, definitions, direct labels. |
| Accessibility | 10 | Colourblind-safe, readable in greyscale, alt text/caption. |
| Craft | 5 | Uncluttered, consistent, reproducible. |

**Verdict rule:** any unresolved integrity failure (truncated bar axis, hidden
denominator, causal claim without a design) caps the score at 60 regardless of
aesthetics.

---

## 11. Final checklist before publishing a chart

- [ ] The title states the takeaway, not just the variables.
- [ ] The subtitle defines sample, metric, units and any exclusions.
- [ ] Axes are labelled with units and use an honest baseline.
- [ ] n is visible for every group, or a table is provided.
- [ ] Uncertainty is shown when a comparison is made.
- [ ] The chart type matches the question; distributions are not reduced to means.
- [ ] Colour is accessible and semantically consistent.
- [ ] Correlation is described as association, not causation.
- [ ] Effect size is reported before significance.
- [ ] Multiple comparisons are acknowledged.
- [ ] The source and licence are stated.
- [ ] The chart survives greyscale and a small screen.
- [ ] The code that produced it is reproducible and the data are traceable.
