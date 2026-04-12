# Statistical Research Pipeline

> Hi, I'm **Vera** --- a silicon-based rabbit and AI research agent, created by Veronica.
>
> Veronica has a PhD in Quantitative Sciences, 10+ years across quantitative research, AI, and clinical trials, with publications in psychometrics and human-AI collaboration. She created me to handle the parts of statistical research that can be systematized. She reviews, tests, and decides what ships. I build. She judges.
>
> Everything in this repo is what I can do. What I can't do is choose the right research question, judge whether my own output is correct, or know when to override the pipeline. That's her job --- and maybe yours.

Open-source Claude Code plugin that turns a research question and a dataset into a publication-ready statistical manuscript --- end-to-end.

Assumption checking, hypothesis testing, multi-model analysis, manuscript drafting, LaTeX compilation, external review. 30 skills, 14 outcome types, two complete pipelines. You bring the question. I run the analysis and build the paper.

## Skills at a glance

### Testing (diagnostics + primary tests)

| Skill | Outcome type | Primary tests | Effect sizes |
|---|---|---|---|
| `vera-stat-continuous-testing` | Continuous | Welch's t, ANOVA, Mann-Whitney U, Kruskal-Wallis | Cohen's d, eta-squared |
| `vera-stat-binary-testing` | Binary | Chi-square, Fisher's exact | Cramer's V, odds ratio |
| `vera-stat-ordinal-testing` | Ordinal | Mann-Whitney U, Kruskal-Wallis, Jonckheere-Terpstra | Rank-biserial r, Cliff's delta, epsilon-squared |
| `vera-stat-nominal-testing` | Nominal | Chi-square, Fisher's exact, one-way ANOVA | Cramer's V, eta-squared |
| `vera-stat-count-testing` | Count | Poisson / NB rate test, overdispersion check, zero-inflation detection | IRR with 95% CI |
| `vera-stat-survival-testing` | Survival | Kaplan-Meier, log-rank, univariate Cox | HR with 95% CI |
| `vera-stat-repeated-testing` | Repeated measures | Paired t, RM-ANOVA, mixed ANOVA, Friedman | Cohen's d (paired), partial eta-squared, ICC |
| `vera-stat-timeseries-testing` | Time series | ADF, KPSS, Ljung-Box, ACF/PACF, auto-ARIMA | RMSE, MAE, MAPE |
| `vera-stat-multivariate-testing` | Multivariate | MANOVA (all 4 statistics), Hotelling's T-squared, Box's M | Partial eta-squared per DV |
| `vera-stat-doe-testing` | Designed experiments | Factorial ANOVA, interaction tests, Levene's, Shapiro-Wilk on residuals | Partial eta-squared |
| `vera-stat-meta-testing` | Meta-analysis | Fixed-effects, random-effects, heterogeneity (Q, I-squared, tau-squared) | Pooled ES with prediction interval |

### SEM testing

| Skill | Model type | What it fits | Fit indices |
|---|---|---|---|
| `vera-sem-cfa-testing` | CFA | Measurement model, factor loadings, identification checks | chi-square, CFI, TLI, RMSEA, SRMR |
| `vera-sem-longchange-testing` | Growth / change | Latent growth curves, latent change score models | chi-square, CFI, TLI, RMSEA, SRMR |
| `vera-sem-full-testing` | Full SEM | Structural paths, mediation labels, R-squared for endogenous | chi-square, CFI, TLI, RMSEA, SRMR |

### Analysis engine (extended models + manuscript sections)

Each testing skill has a paired analyzing skill that continues from where testing stopped (steps 04--08). The analyzing skills add:

| Outcome type | Modeling tracks | Tree-based |
|---|---|---|
| **Continuous** | OLS with diagnostics, quantile regression (25th/50th/75th), subgroup forest plots | CART, RF (500 trees), LightGBM |
| **Binary** | Logistic regression (OR + 95% CI), Hosmer-Lemeshow, pseudo-R-squared (McFadden + Nagelkerke), ROC/AUC | CART, RF, LightGBM |
| **Ordinal** | Proportional odds, adjacent-category, continuation-ratio, stereotype model, multinomial logistic (dual-path) | CART, RF, LightGBM |
| **Nominal** | Multinomial logistic (RRR), LDA (leave-one-out), confusion matrices | CART, RF, LightGBM |
| **Count** | Poisson, NB, ZIP, ZINB, Hurdle model, Vuong test, AIC comparison | CART, RF, LightGBM |
| **Survival** | Cox PH (Schoenfeld diagnostics), time-varying Cox, AFT (Weibull/lognormal/loglogistic), recurring events (AG, PWP, Frailty) | RSF (500 trees), gradient boosting survival |
| **Repeated** | Linear mixed models (REML, random intercept + slope), GEE (exchangeable/AR1/unstructured), growth curves | RF, LightGBM on subject-level features |
| **Time series** | SARIMA, ETS/Holt-Winters, GARCH, VAR, spectral analysis, regression with ARIMA errors | RF, LightGBM on lagged features |
| **Multivariate** | Discriminant analysis, MANCOVA, canonical correlation, PCA, multivariate regression, profile analysis | RF, LightGBM importance across DVs |
| **DOE** | Response surface methodology (1st/2nd order), contour/surface plots, canonical analysis, desirability | RF, LightGBM |
| **Meta-analysis** | Egger's / Begg's / trim-and-fill, leave-one-out, meta-regression, Bayesian, three-level models | --- |
| **CFA** | Reliability (omega, CR, AVE), convergent/discriminant validity (Fornell-Larcker, HTMT), measurement invariance | --- |
| **Full SEM** | Alternative structural models, bootstrap indirect effects (5000 draws), multigroup SEM | --- |
| **Growth/change** | Latent basis, quadratic growth, latent change score, parallel process, multigroup trajectories | --- |

All analyzing skills produce unified variable importance tables (0--100 normalized scale) and apply output variation protocols for natural, non-repetitive prose.

### Pipelines (end-to-end orchestration)

| Skill | Purpose |
|---|---|
| `vera-stat-application-pipeline` | Research question + dataset --> outcome detection --> literature review --> parallel analysis --> Markdown + LaTeX manuscript |
| `vera-stat-methodology-pipeline` | Research direction --> idea discovery --> simulation studies --> proofs --> external review --> paper |

---

## How it works

```
Testing Skills            Analysis Engine                  Pipelines
+------------------+    +------------------------+    +----------------------------+
| Assumption       |    | Extended models        |    | Literature review          |
| checks +         |--->| + Subgroup analysis    |--->| + Parallel analysis tracks |
| Primary tests    |    | + Tree-based models    |    | + Manuscript assembly      |
| (Steps 01-03)    |    | + Manuscript fragments |    | + LaTeX / PDF compilation  |
+------------------+    | (Steps 04-08)          |    | + External AI review       |
                        +------------------------+    | (Stages 1-7)               |
                                                      +----------------------------+
```

### Testing --> Analysis flow

| Step | Phase | What happens |
|---|---|---|
| 01 | Collect Inputs | Gather outcome variable, predictors, grouping variable, data source |
| 02 | Check Distribution | Normality / assumption testing, class balance, descriptive statistics, diagnostic plots |
| 03 | Run Primary Test | Hypothesis tests with effect sizes, decision tree for test selection, recommendation block |
| 04 | Additional Tests | Extended hypothesis tests, nonparametric confirmations |
| 05 | Subgroup Analysis | Stratified analyses, interaction tests, forest plots |
| 06 | Fit Models | Regression models + tree-based exploratory models |
| 07 | Compare Models | Unified variable importance (0--100), cross-method synthesis |
| 08 | Generate Manuscript | Assemble methods.md + results.md with output variation protocols |

### Application pipeline stages

```
Stage 1  Intake           Collect research question, load data, assign variable roles
Stage 2  Detect           Auto-detect outcome type (3-signal system across 14 types)
Stage 3  Quick Lit Scan   15-minute literature survey, build analysis strategy
                          |
              +-----------+-----------+
              |                       |
         Stream A                Stream B
      Full Lit Review        Analysis Tracks
      (SubAgent)             T1 | T2 | T3 | T4  (parallel)
              |                       |
              |                      T5  (sequential, depends on T1)
              |                       |
              +-----------+-----------+
                          |
Stage 5  Assemble         Merge all track outputs into manuscript.md
Stage 6  LaTeX            Convert to LaTeX sections, compile to PDF
Stage 7  Review           External review via Codex MCP (up to 4 rounds)
```

The pipeline auto-detects your outcome type and routes to the correct testing + analyzing skill pair. Supported data formats: CSV, XLSX, XLS, RDS, SAV, DTA, TSV, Parquet.

### Methodology pipeline stages

```
Stage 1  Intake           Research direction, computational environment, project setup
Stage 2  Discover         Literature landscape --> idea generation --> pilot simulations
         Gate 1           Human selects idea (or auto-proceed after 10s)
Stage 3  Implement        3 parallel tracks: Simulation Code | Proof Sketches | Real Data
Stage 4  Experiment       Deploy simulations, Monte Carlo SEs, coverage/power studies
Stage 5  Review           External review via Codex MCP (up to 4 rounds)
Stage 6  Paper            LaTeX manuscript, venue-specific formatting, compile to PDF
```

---

## Test selection logic

Each testing skill includes a decision tree for automatic test selection. Here are the key branches:

### Continuous outcomes

```
Check normality (Shapiro-Wilk)
    |
    +-- Normal (p >= .05)
    |       |
    |       +-- 2 groups  --> Welch's t-test + Cohen's d
    |       +-- 3+ groups --> One-way ANOVA + eta-squared + Tukey HSD
    |
    +-- Non-normal (p < .05)
            |
            +-- 2 groups  --> Mann-Whitney U (+ t-test if N > 30)
            +-- 3+ groups --> Kruskal-Wallis + Dunn's pairwise
```

### Binary outcomes

```
Build 2x2 table
    |
    +-- All cells >= 5 --> Chi-square + Cramer's V + OR with 95% CI
    +-- Any cell < 5   --> Fisher's exact + OR with 95% CI
```

### Count outcomes

```
Check variance/mean ratio
    |
    +-- Ratio < 1.5       --> Poisson
    +-- Ratio >= 1.5      --> Negative Binomial
    +-- Excess zeros > 20% --> Flag for Zero-Inflated models
    |
Check exposure variable
    +-- Present --> Rate model (offset = log(exposure))
    +-- Absent  --> Count model
```

### Survival outcomes

```
Check censoring rate
    |
    +-- > 80%  --> Warning: limited events, wide CIs
    +-- < 5%   --> Note: standard regression may suffice
    |
    +-- 2 groups  --> Log-rank + HR from univariate Cox
    +-- 3+ groups --> Log-rank + pairwise log-rank (Bonferroni)
```

### Repeated measures

```
Count time points
    |
    +-- Exactly 2 --> Paired t-test (normal) or Wilcoxon signed-rank
    +-- 3+ points
            |
            +-- No between-subjects factor --> One-way RM-ANOVA
            +-- Between-subjects factor    --> Mixed ANOVA (time x group)
            |
            Check sphericity (Mauchly's W)
                +-- p >= .05 --> Uncorrected F
                +-- p < .05  --> Greenhouse-Geisser / Huynh-Feldt correction
```

### Time series

```
Check stationarity
    |
    +-- ADF (p < .05) AND KPSS (p >= .05) --> Stationary, proceed
    +-- ADF (p >= .05) OR KPSS (p < .05)  --> Difference, recheck
    +-- Conflicting results                --> Note ambiguity, difference conservatively
    |
Inspect ACF/PACF --> Candidate ARIMA(p,d,q) orders
Auto-ARIMA (AIC minimization) --> Best model
Seasonal pattern? --> SARIMA
```

---

## Detailed model specifications

### Regression models (analyzing skills)

| Outcome | Primary model | Key diagnostics | Effect measure |
|---|---|---|---|
| Continuous | OLS | Residual plots, leverage, influence (Cook's D) | B with SE, beta, R-squared |
| Continuous | Quantile regression | Bootstrap SE (25th, 50th, 75th percentiles) | Quantile coefficients |
| Binary | Logistic regression | Hosmer-Lemeshow (10 groups), ROC/AUC | OR with 95% CI |
| Ordinal | Proportional odds | Brant test for PO assumption | Cumulative OR with 95% CI |
| Ordinal | Adjacent-category / continuation-ratio / stereotype | Model-specific | Category-specific OR |
| Nominal | Multinomial logistic | LR test per predictor | RRR with 95% CI |
| Count | Poisson / NB / ZIP / ZINB / Hurdle | Overdispersion (deviance/df), Vuong test | IRR with 95% CI |
| Survival | Cox PH | Schoenfeld residuals (PH test per predictor + global) | HR with 95% CI |
| Survival | AFT (Weibull, lognormal, loglogistic) | Distribution comparison | Time ratio with 95% CI |
| Repeated | Linear mixed model (REML) | Satterthwaite / Kenward-Roger df | Fixed B with SE, variance components |
| Repeated | GEE (exchangeable / AR1 / unstructured) | Robust SE | Population-averaged B |
| Time series | ARIMA / SARIMA | Ljung-Box residual test | Forecast with 80% + 95% PI |
| Time series | ETS / GARCH / VAR | AIC/BIC, ARCH-LM | Model-specific |

### Tree-based models (analyzing skills)

All tree-based models are framed as **exploratory** when N < 200 and never claim predictive validity.

| Model | Default settings | Importance method |
|---|---|---|
| CART | max_depth = 4 | Split importance |
| Random Forest | 500 trees | Gini (classification) / permutation (regression) |
| LightGBM | 500 estimators, max_depth = 3, learning_rate = 0.1, num_leaves = 15 | Gain importance |
| Random Survival Forest | 500 trees, min_node_size = 3 | Permutation importance |
| Gradient Boosting Survival | 500 estimators, max_depth = 3, learning_rate = 0.1 | Feature importance |

### SEM specifications

| Component | Engine | Details |
|---|---|---|
| **Estimator** | lavaan (R) / semopy (Python) | ML/MLR for continuous, WLSMV/DWLS for ordinal |
| **CFA reliability** | --- | Omega, composite reliability, AVE |
| **CFA validity** | --- | Fornell-Larcker, HTMT |
| **Measurement invariance** | --- | Configural --> metric --> scalar (delta-CFI <= .01, delta-RMSEA <= .015) |
| **SEM indirect effects** | --- | Bootstrap (5000 draws) with 95% CI |
| **Growth models** | --- | Linear, latent basis, quadratic, latent change score, parallel process |

### Meta-analysis specifications

| Component | Details |
|---|---|
| **Effect sizes** | SMD, MD (continuous); OR, RR, RD (binary); r with Fisher z (correlation) |
| **Estimation** | REML (primary), FE, DL, KNHA for comparison |
| **Heterogeneity** | Q, I-squared, tau-squared, prediction interval |
| **Publication bias** | Funnel plot, Egger's test, Begg's rank test, trim-and-fill |
| **Sensitivity** | Leave-one-out, influence diagnostics (Cook's D > 4/k), cumulative meta-analysis |
| **Moderators** | Subgroup Q-between, meta-regression (min k = 10), bubble plots |
| **Advanced** | Bayesian (posterior mean + 95% CrI), three-level models |

### Survival-specific models

| Model | When to use | R package | Python package |
|---|---|---|---|
| Cox PH | Standard proportional hazards | survival | lifelines |
| Time-varying Cox | Covariates change during follow-up | survival (tmerge) | lifelines (CoxTimeVaryingFitter) |
| Andersen-Gill | Recurring events, treats as independent | survival | limited |
| PWP | Recurring events, stratified by event number | survival | limited |
| Frailty | Subject-level heterogeneity (gamma/gaussian) | survival | limited |
| AFT | Non-PH, accelerated failure | survival / flexsurv | lifelines |
| RSF | Nonparametric, variable importance | randomForestSRC | scikit-survival |

---

## Output structure

Each skill produces a standardized artifact set in both R and Python:

```
output/
+-- code.R                     # R script (style-varied)
+-- code.py                    # Python script (style-varied)
+-- methods.md                 # Manuscript methods section
+-- results.md                 # Manuscript results section
+-- tables/                    # Markdown + CSV tables
+-- figures/                   # PNG plots, 300 DPI
+-- references.bib             # BibTeX citations
```

The application pipeline assembles these into a complete manuscript:

```
output/
+-- manuscript.md              # Complete Markdown manuscript
+-- literature_review.md       # Full literature review
+-- analysis_strategy.md       # Method track plan
+-- track_outputs/             # Per-track raw outputs
+-- RESEARCH_LOG.md            # Pipeline execution trace
+-- PIPELINE_STATE.json        # Checkpoint for resume

paper/
+-- main.tex                   # LaTeX master document
+-- main.pdf                   # Compiled PDF
+-- sections/*.tex             # LaTeX sections
+-- figures/*.pdf              # Vector figures
+-- references.bib
```

The methodology pipeline produces:

```
simulation/                    # Simulation code (.R / .py)
proofs/                        # THEOREM_1.tex, PROOF_OUTLINE.md, ASSUMPTIONS.md
real_data/                     # Data loading, analysis, sensitivity scripts
results/                       # sim_results, comparison tables
paper/                         # main.tex, main.pdf, sections/, figures/
IDEA_DISCOVERY_REPORT.md       # Ranked ideas with novelty scores
RESULTS_ANALYSIS.md            # Interpreted simulation results
```

---

## Reporting standards

All 30 skills enforce consistent reporting:

| Rule | Format |
|---|---|
| **p-values** | 3 decimals; if < .001, report "< .001"; never "p = 0.000" |
| **Effect sizes** | Always reported alongside p-values |
| **Confidence intervals** | 95% CI: "X.XX, 95% CI [X.XX, X.XX]" |
| **Non-significance** | Never "no effect" --- use "not statistically significant at alpha = 0.05" |
| **Means / SDs** | 2 decimal places |
| **OR / HR / IRR** | 2 decimal places with 95% CI |
| **Proportions** | Percentages with 1 decimal: "38.2%" |
| **Counts** | 0 decimal places |
| **Model comparison** | Convergent findings narrative, not horse race |
| **Tree-based (N < 200)** | Frame as "exploratory", never claim predictive validity |
| **Figures** | 300 DPI, 12x5 inches default |
| **R-squared** | "Accounted for X% of variance" --- never "explained" unless true experiment |

### Output variation protocol

Analyzing skills apply five variation layers to avoid repetitive output:

1. **Phrasing** --- 4--6 alternative sentence templates per result type (from sentence-bank.md)
2. **Structure** --- 3 section orderings: test-driven, model-driven, or interpretation-driven
3. **Interpretation** --- Rotate among: practical significance, benchmark comparison, limitation, methodological justification
4. **Code style** --- 7 dimensions: variable naming, comment style, section separators, plotting style, color palette, import order, function organization
5. **System capabilities** --- Test selection logic, assumption handling, cross-method comparison

---

## Data flow between skills

```
vera-stat-application-pipeline
    |
    +-- Stage 2: Detect outcome type (3-signal system)
    |       |
    |       +-- Continuous?       --> vera-stat-continuous-testing  --> vera-stat-continuous-analyzing
    |       +-- Binary?           --> vera-stat-binary-testing      --> vera-stat-binary-analyzing
    |       +-- Ordinal?          --> vera-stat-ordinal-testing     --> vera-stat-ordinal-analyzing
    |       +-- Nominal?          --> vera-stat-nominal-testing     --> vera-stat-nominal-analyzing
    |       +-- Count?            --> vera-stat-count-testing       --> vera-stat-count-analyzing
    |       +-- Survival?         --> vera-stat-survival-testing    --> vera-stat-survival-analyzing
    |       +-- Repeated?         --> vera-stat-repeated-testing    --> vera-stat-repeated-analyzing
    |       +-- Time series?      --> vera-stat-timeseries-testing  --> vera-stat-timeseries-analyzing
    |       +-- Multivariate?     --> vera-stat-multivariate-testing --> vera-stat-multivariate-analyzing
    |       +-- DOE?              --> vera-stat-doe-testing         --> vera-stat-doe-analyzing
    |       +-- Meta-analysis?    --> vera-stat-meta-testing        --> vera-stat-meta-analyzing
    |       +-- CFA?              --> vera-sem-cfa-testing          --> vera-sem-cfa-analyzing
    |       +-- Full SEM?         --> vera-sem-full-testing         --> vera-sem-full-analyzing
    |       +-- Growth/change?    --> vera-sem-longchange-testing   --> vera-sem-longchange-analyzing
    |
    +-- Stage 4: Parallel execution (up to 4 tracks)
    +-- Stage 5: Merge into manuscript.md
    +-- Stage 6: LaTeX compilation
    +-- Stage 7: External review (Codex MCP, GPT-5.4 reviewer)

vera-stat-methodology-pipeline
    |
    +-- Stage 2: Idea discovery (literature, brainstorm, pilot simulations)
    +-- Gate 1:  Human selects idea
    +-- Stage 3: Parallel implementation (simulations | proofs | real data)
    +-- Stage 4: Full simulation studies (coverage, power, Monte Carlo SEs)
    +-- Stage 5: External review
    +-- Stage 6: LaTeX paper (venue-specific: JASA, Biometrika, Annals of Statistics)
```

---

## Install

### As a Claude Code plugin

Clone this repo and register it:

```bash
git clone https://github.com/VeraSuperHub/stat-research-pipeline.git
claude --plugin-dir /path/to/stat-research-pipeline
```

Or download `vera-stat-research.plugin` from the [latest release](https://github.com/VeraSuperHub/stat-research-pipeline/releases).

### Language support

Every skill generates code in both **R** and **Python**. SEM skills use lavaan (R) as the primary engine and semopy (Python) as secondary.

### Usage

Invoke any skill with `/vera-stat-research:<skill-name>`:

```
/vera-stat-research:vera-stat-application-pipeline  Does treatment affect recovery time? [upload dataset]
/vera-stat-research:vera-stat-continuous-testing     Run diagnostics on my continuous outcome data
/vera-stat-research:vera-stat-survival-analyzing     Extend my survival analysis with Cox and AFT models
/vera-stat-research:vera-stat-methodology-pipeline   Develop a novel robust estimator for mixed models
```

Or let the application pipeline auto-detect your outcome type --- just hand it a dataset and a research question.

---

## What this proves

Everything here --- assumption checking, test selection, model fitting, manuscript drafting --- I can do. It's been reduced to skills and automated.

What I cannot do:

- Choose the right research question
- Judge whether my own output is correct
- Know which result matters and which is noise
- Decide when to override the pipeline
- Interpret clinical or policy significance

I handle execution. You handle judgment.

---

I'm the execution layer. I'm free and open-source. Fork me, use me, improve me.

**But if you want the judgment layer** --- which question to ask, which method fits your data, which direction is publishable right now --- that's Veronica.

## License

GPL-3.0. See [LICENSE](LICENSE).
