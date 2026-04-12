# Statistical Research Pipeline

> Hi, I'm **Vera** — a silicon-based rabbit and AI research agent, created by Veronica.
>
> Veronica has a PhD in Quantitative Sciences, 10+ years across quantitative research, AI, and clinical trials, with publications in psychometrics and human-AI collaboration. She created me to handle the parts of statistical research that can be systematized. She reviews, tests, and decides what ships. I build. She judges.
>
> Everything in this repo is what I can do. What I can't do is choose the right research question, judge whether my own output is correct, or know when to override the pipeline. That's her job — and maybe yours.

Open-source Claude Code skills that turn a research question and a dataset into a publication-ready statistical manuscript — end-to-end.

Assumption checking, hypothesis testing, multi-model analysis, manuscript drafting, LaTeX compilation, external review. 30 skills, 14 outcome types, two complete pipelines. You bring the question. I run the analysis and build the paper.

## What's here

### Testing (diagnostics + primary tests)

| Skill | Outcome type | What it does |
|---|---|---|
| `vera-stat-continuous-testing` | Continuous | Normality, t-test, ANOVA, Mann-Whitney, effect sizes |
| `vera-stat-binary-testing` | Binary | Chi-square, Fisher's exact, odds ratios with CIs |
| `vera-stat-ordinal-testing` | Ordinal | Mann-Whitney U, Kruskal-Wallis, Jonckheere-Terpstra, rank-biserial |
| `vera-stat-nominal-testing` | Nominal | Chi-square, Cramer's V, multi-category diagnostics |
| `vera-stat-count-testing` | Count | Poisson/NB, zero-inflation detection, overdispersion |
| `vera-stat-survival-testing` | Survival | Kaplan-Meier, log-rank, univariate Cox, number-at-risk |
| `vera-stat-repeated-testing` | Repeated measures | Paired t, RM-ANOVA, mixed ANOVA, ICC, sphericity |
| `vera-stat-timeseries-testing` | Time series | ACF/PACF, ADF/KPSS, Ljung-Box, stationarity |
| `vera-stat-multivariate-testing` | Multivariate | MANOVA, Hotelling's T-squared, Box's M |
| `vera-stat-doe-testing` | Designed experiments | Factorial, fractional factorial |
| `vera-stat-meta-testing` | Meta-analysis | Effect sizes, heterogeneity, forest plots |

### SEM testing

| Skill | Model type | What it does |
|---|---|---|
| `vera-sem-cfa-testing` | CFA | Measurement model fit, factor loadings, identification checks |
| `vera-sem-longchange-testing` | Growth/change | Latent growth models, latent change score models |
| `vera-sem-full-testing` | Full SEM | Structural paths, mediation, global fit |

### Analysis engine (extended models + manuscript sections)

Each testing skill has a paired analyzing skill that extends with OLS, quantile regression, tree-based models (CART, Random Forest, LightGBM), cross-method comparison, subgroup analysis, and manuscript-ready methods/results fragments.

### Pipelines (end-to-end orchestration)

| Skill | Purpose |
|---|---|
| `vera-stat-application-pipeline` | Research question + dataset -> outcome detection -> literature review -> parallel analysis -> Markdown + LaTeX manuscript |
| `vera-stat-methodology-pipeline` | Research direction -> idea discovery -> simulation studies -> proofs -> external review -> paper |

## How it works

```
Testing Skills          Analysis Engine              Pipelines
+----------------+    +----------------------+    +--------------------------+
| Assumptions    |--->| Extended models      |--->| Literature + Analysis    |
| + Primary      |    | + Manuscript parts   |    | + Manuscript + LaTeX     |
|   tests        |    | + Subgroups          |    | + External review        |
+----------------+    +----------------------+    +--------------------------+
  Steps 01-03            Steps 04-08                Stages 1-7
```

The application pipeline auto-detects your outcome type (continuous, binary, ordinal, survival, etc.) and routes to the correct testing + analyzing skill pair. You don't need to pick — just hand it a dataset and a question.

## Install

Drop any skill folder into your Claude Code skill directory, or clone this repo and point Claude Code at the skill you need.

Languages: R and Python. Each skill generates code in both.

## What this proves

Everything here — assumption checking, test selection, model fitting, manuscript drafting — I can do. It's been reduced to skills and automated.

What I cannot do:

- Choose the right research question
- Judge whether my own output is correct
- Know which result matters and which is noise
- Decide when to override the pipeline
- Interpret clinical or policy significance

I handle execution. You handle judgment.
