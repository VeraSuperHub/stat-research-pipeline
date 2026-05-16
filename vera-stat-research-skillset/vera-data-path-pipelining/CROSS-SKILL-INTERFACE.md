# Cross-Skill Interface

This repository uses paired reviewing and generating skills.

## Handoff Contract

The reviewing skill owns input collection, assumption checks, primary-test
readiness, and baseline evidence. The generating skill owns extended tests,
modeling, subgroup analysis, comparison, and manuscript-section artifact
generation.

A pipeline handoff should preserve these fields in `PIPELINE_STATE.json` when
available:

- `outcome_type`
- `testing_skill_path` or reviewing skill path
- `analysis_skill_path` or generating skill path
- `data_file`
- outcome, predictor, grouping, covariate, and subgroup metadata
- `method_tracks`
- output directories and any assumption/primary-test artifacts already produced

If a generating skill is invoked directly and these artifacts are missing, it
should stop and ask for the missing data/context instead of inventing upstream
results.

## Flattened Skillset Layout

The published repository uses flat sibling directories such as
`vera-data-continuous-reviewing/` and `vera-data-continuous-generating/`.
References to older nested `vera-data-analysis-engine/...` paths should be
interpreted as the same generating skill in the flat skillset.
