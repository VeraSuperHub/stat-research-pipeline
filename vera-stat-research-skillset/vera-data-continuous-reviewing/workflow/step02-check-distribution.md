# 02 — Check Distribution

## Executor: Main Agent (code generation)

## Data In: Structured input summary from 01-collect-inputs.md

## Generate code for PART 1

### Tests
- Shapiro-Wilk normality test on **residuals from the group-mean model** (i.e., `residuals = Y − group_mean`), NOT on raw Y. The t-test / ANOVA normality assumption is about residuals, not the marginal distribution of Y. For a single-group diagnostic with no grouping factor, residuals collapse to Y − grand_mean and the two are equivalent.
- Also report Shapiro-Wilk on raw Y as a supplementary diagnostic.
- Skewness (scipy.stats.skew / moments::skewness) — on residuals
- Kurtosis (excess kurtosis in Python, regular in R — note the difference) — on residuals
- Levene's test (F, p) on group variances using the median-centered form (more robust than mean-centered)

### Descriptive statistics
- Mean, SD, Min, Max, N (non-missing)
- If groups exist: descriptives per group

### Plots
- Histogram with kernel density overlay
- Q-Q plot against normal distribution
- Save as `plot_01_distribution.png` (side-by-side, 12x5, 300 DPI)

### Decision logic (printed in console)

```
if N > 200:
    # Shapiro-Wilk is over-sensitive at large N; rely on magnitudes + Q-Q plot
    if |skewness_residuals| < 1 AND |excess_kurtosis_residuals| < 2 AND Q-Q plot visually linear:
        → "Residuals approximately normal by shape; Shapiro-Wilk p reported but de-emphasized given N."
        → normality_flag = TRUE
    else:
        → normality_flag = FALSE
else:
    if Shapiro-Wilk p (on residuals) >= 0.05 AND |skewness_residuals| < 1:
        → "Residuals approximately normal. OLS/t-test/ANOVA appropriate."
        → normality_flag = TRUE
    else:
        → "Residuals deviate from normal. Consider transformation or nonparametric."
        → normality_flag = FALSE

# Levene's decision for variance homogeneity
if Levene's p >= 0.05:
    → equal_variance_flag = TRUE   # can use Student's t / pooled ANOVA / Tukey HSD
else:
    → equal_variance_flag = FALSE  # use Welch's t / Welch ANOVA / Games-Howell post-hoc
```

### Interpretation
Print 2 sentences: distribution shape + test results, then decision and rationale.

## Validation Checkpoint

- [ ] Shapiro-Wilk W and p reported
- [ ] Skewness and kurtosis reported
- [ ] Descriptive stats complete (M, SD, min, max, N)
- [ ] plot_01_distribution.png generated
- [ ] normality_flag set (TRUE/FALSE)
- [ ] Decision statement printed

## Data Out → 03-run-primary-test.md

```
normality_flag: TRUE | FALSE
descriptives: {mean, sd, min, max, n}
distribution_code_r: [PART 1 R code block]
distribution_code_py: [PART 1 Python code block]
```
