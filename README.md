# Statistical Research Pipeline

Open-source statistical research skills for Claude Code and Codex-compatible workflows.

This repository packages the Vera data/statistical research skill family for outcome detection, assumption checks, primary test selection, extended modeling, SEM workflows, manuscript-section drafting, LaTeX-ready artifact assembly, and review checkpoints.

Vera structures the execution layer. Researchers own study design, assumptions, interpretation, and submission decisions.

## Skill Inventory

### Reviewing Skills

| Skill | Domain | Role |
|---|---|---|
| `vera-data-binary-reviewing` | Binary | Review inputs, assumptions, primary-test readiness, reporting constraints, and evidence quality. |
| `vera-data-cfa-reviewing` | CFA | Review inputs, assumptions, primary-test readiness, reporting constraints, and evidence quality. |
| `vera-data-continuous-reviewing` | Continuous | Review inputs, assumptions, primary-test readiness, reporting constraints, and evidence quality. |
| `vera-data-count-reviewing` | Count | Review inputs, assumptions, primary-test readiness, reporting constraints, and evidence quality. |
| `vera-data-doe-reviewing` | DOE | Review inputs, assumptions, primary-test readiness, reporting constraints, and evidence quality. |
| `vera-data-growth-reviewing` | Growth/change | Review inputs, assumptions, primary-test readiness, reporting constraints, and evidence quality. |
| `vera-data-meta-reviewing` | Meta-analysis | Review inputs, assumptions, primary-test readiness, reporting constraints, and evidence quality. |
| `vera-data-multivariate-reviewing` | Multivariate | Review inputs, assumptions, primary-test readiness, reporting constraints, and evidence quality. |
| `vera-data-nominal-reviewing` | Nominal | Review inputs, assumptions, primary-test readiness, reporting constraints, and evidence quality. |
| `vera-data-ordinal-reviewing` | Ordinal | Review inputs, assumptions, primary-test readiness, reporting constraints, and evidence quality. |
| `vera-data-path-reviewing` | SEM path | Review inputs, assumptions, primary-test readiness, reporting constraints, and evidence quality. |
| `vera-data-repeated-reviewing` | Repeated | Review inputs, assumptions, primary-test readiness, reporting constraints, and evidence quality. |
| `vera-data-survival-reviewing` | Survival | Review inputs, assumptions, primary-test readiness, reporting constraints, and evidence quality. |
| `vera-data-timeseries-reviewing` | Time series | Review inputs, assumptions, primary-test readiness, reporting constraints, and evidence quality. |

### Generating Skills

| Skill | Domain | Role |
|---|---|---|
| `vera-data-binary-generating` | Binary | Run extended model workflows and generate methods/results artifacts with traceable outputs. |
| `vera-data-cfa-generating` | CFA | Run extended model workflows and generate methods/results artifacts with traceable outputs. |
| `vera-data-continuous-generating` | Continuous | Run extended model workflows and generate methods/results artifacts with traceable outputs. |
| `vera-data-count-generating` | Count | Run extended model workflows and generate methods/results artifacts with traceable outputs. |
| `vera-data-doe-generating` | DOE | Run extended model workflows and generate methods/results artifacts with traceable outputs. |
| `vera-data-growth-generating` | Growth/change | Run extended model workflows and generate methods/results artifacts with traceable outputs. |
| `vera-data-meta-generating` | Meta-analysis | Run extended model workflows and generate methods/results artifacts with traceable outputs. |
| `vera-data-multivariate-generating` | Multivariate | Run extended model workflows and generate methods/results artifacts with traceable outputs. |
| `vera-data-nominal-generating` | Nominal | Run extended model workflows and generate methods/results artifacts with traceable outputs. |
| `vera-data-ordinal-generating` | Ordinal | Run extended model workflows and generate methods/results artifacts with traceable outputs. |
| `vera-data-path-generating` | SEM path | Run extended model workflows and generate methods/results artifacts with traceable outputs. |
| `vera-data-repeated-generating` | Repeated | Run extended model workflows and generate methods/results artifacts with traceable outputs. |
| `vera-data-survival-generating` | Survival | Run extended model workflows and generate methods/results artifacts with traceable outputs. |
| `vera-data-timeseries-generating` | Time series | Run extended model workflows and generate methods/results artifacts with traceable outputs. |

### Pipeline Skills

| Skill | Workflow | Role |
|---|---|---|
| `vera-data-application-pipelining` | Application | Coordinate multi-step statistical research execution, artifact assembly, and review checkpoints. |
| `vera-data-cfa-pipelining` | CFA | Coordinate multi-step statistical research execution, artifact assembly, and review checkpoints. |
| `vera-data-growth-pipelining` | Growth/change | Coordinate multi-step statistical research execution, artifact assembly, and review checkpoints. |
| `vera-data-methodology-pipelining` | Methodology | Coordinate multi-step statistical research execution, artifact assembly, and review checkpoints. |
| `vera-data-path-pipelining` | SEM path | Coordinate multi-step statistical research execution, artifact assembly, and review checkpoints. |

## Install

Clone the repository:

```bash
git clone https://github.com/VeraSuperHub/stat-research-pipeline.git
```

Claude Code users can import `vera-stat-research.plugin` with the Claude Code plugin flow.

Codex users can install the extracted skill folders directly:

```bash
mkdir -p ~/.codex/skills
cp -R vera-stat-research-skillset/vera-data-* ~/.codex/skills/
```

You can also copy a single folder from `vera-stat-research-skillset/` if you only need one skill.

## Repository Contents

| Path | Purpose |
|---|---|
| `vera-stat-research-skillset/` | Extracted skill folders for direct inspection, editing, or Codex installation. |
| `vera-stat-research.plugin` | Claude Code plugin bundle rebuilt from the same extracted skills. |
| `PLATFORM-COMPATIBILITY.md` | Runtime mapping for Claude Code, Codex, and fallback behavior. |
| `CROSS-SKILL-INTERFACE.md` | Handoff contract between reviewing and generating skills. |

## Workflow Shape

```text
Reviewing skills -> Generating skills -> Pipeline skills
      |                    |                   |
 assumptions       extended models       manuscript assembly
 primary tests     comparisons           review checkpoints
```

The skills are designed to support reproducible statistical execution, not to replace statistical judgment. Treat generated methods, results, and interpretation drafts as reviewable artifacts that need domain-owner approval before use.

## License

GPL-3.0. See [LICENSE](LICENSE).
