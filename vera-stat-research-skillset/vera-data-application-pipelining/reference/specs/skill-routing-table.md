# Skill Routing Table

Maps confirmed outcome type to the paired reviewing and generating skill paths.

All paths are relative to `REPO_ROOT`, the directory that contains the extracted
`vera-stat-research-skillset/` contents. In this repository and in a direct
Codex install, the skills are flat sibling directories such as
`vera-data-continuous-reviewing/` and `vera-data-continuous-generating/`.

Do not prepend `vera-data-analysis-engine/`; that was the older source-tree layout.

## Routing Table

| Outcome Type | Reviewing Skill Directory | Generating Skill Directory | Key Methods |
|---|---|---|---|
| continuous | `vera-data-continuous-reviewing/` | `vera-data-continuous-generating/` | OLS, quantile regression, CART/RF/LightGBM |
| binary | `vera-data-binary-reviewing/` | `vera-data-binary-generating/` | Logistic regression, ROC, trees |
| ordinal | `vera-data-ordinal-reviewing/` | `vera-data-ordinal-generating/` | Proportional odds, adjacent-category, trees |
| nominal | `vera-data-nominal-reviewing/` | `vera-data-nominal-generating/` | Multinomial logistic, LDA, trees |
| count | `vera-data-count-reviewing/` | `vera-data-count-generating/` | Poisson, NB, ZIP, ZINB, hurdle |
| survival | `vera-data-survival-reviewing/` | `vera-data-survival-generating/` | Cox PH, AFT, random survival forest |
| repeated | `vera-data-repeated-reviewing/` | `vera-data-repeated-generating/` | Mixed models, GEE, growth curves |
| timeseries | `vera-data-timeseries-reviewing/` | `vera-data-timeseries-generating/` | ARIMA, SARIMA, GARCH, spectral, ML forecasting |
| multivariate | `vera-data-multivariate-reviewing/` | `vera-data-multivariate-generating/` | MANOVA, canonical correlation, PCA |
| doe | `vera-data-doe-reviewing/` | `vera-data-doe-generating/` | Factorial ANOVA, RSM, Taguchi, power analysis |
| meta | `vera-data-meta-reviewing/` | `vera-data-meta-generating/` | Fixed/random effects, meta-regression, forest plots |
| sem-cfa | `vera-data-cfa-reviewing/` | `vera-data-cfa-generating/` | CFA, fit indices, modification indices |
| sem-full | `vera-data-path-reviewing/` | `vera-data-path-generating/` | Full SEM, mediation, moderation, multi-group |
| sem-longchange | `vera-data-growth-reviewing/` | `vera-data-growth-generating/` | Latent growth curves, longitudinal SEM |

## Open-Source Contract

- Treat this table as the public method contract for the applied stats stack.
- The reviewing skill named in each row is the shipped baseline / diagnostics entry point.
- The paired generating skill is the shipped full-analysis extension for that same family.
- If a method family is not named here, do not imply it is supported just because it is statistically adjacent.

## Workflow Files Available Per Skill

Each routed reviewing skill contains:

```text
workflow/step01-collect-inputs.md
workflow/step02-check-distribution.md
workflow/step03-run-primary-test.md
```

Each routed generating skill contains:

```text
workflow/step04-run-additional-tests.md
workflow/step05-analyze-subgroups.md
workflow/step06-fit-models.md
workflow/step07-compare-models.md
workflow/step08-generate-manuscript.md
reference/
```

## How the Pipeline Uses This Table

1. Step 02 confirms the outcome type.
2. Record both the reviewing-skill path and the generating-skill path.
3. Step 04 reads the routed reviewing skill for `T1_primary`.
4. Step 04 reads the routed generating skill for downstream tracks (`T2+`).
5. Track outputs follow the generating skill's output format.
6. Output quality references are read from the generating skill's `reference/` directory.
