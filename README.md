# Let's Encode! — campaign template

This is the **template repository** every campaign is stamped from (via GitHub's
"create a repository from a template"). A copy of it becomes one crowd-encoding
campaign: it holds the score sources, the campaign configuration, two
machine-maintained tracking tables, and the GitHub Actions that run the
workflow.

> You normally don't touch these files by hand. The instigation platform fills
> in the configuration at campaign start, and the volunteer client claims and
> submits work through pull requests. The files are kept human-readable so they
> review cleanly in pull-request diffs.

## Layout

```
config.example.yaml          # campaign config TEMPLATE (schema v1) — documented inline
config.yaml                  # written at instigation by the GUI (not in the template)
sources/
  score.mei                  # written at init from the template below (not in the template)
templates/
  score.template.mei         # barebones MEI: 1 measure, 1 note, header placeholders
tracking/
  state.csv                  # state table — generated & maintained by Actions
  locks.csv                  # lock table — generated & maintained by Actions
.github/workflows/           # campaign Actions (added in a later phase)
```

## Lifecycle in one paragraph

The instigation GUI generates a campaign repo from this template, then commits a
filled-in `config.yaml` (copied from `config.example.yaml`) and places/refers to
the score sources. That commit triggers the **initialisation Action**, which
stamps `templates/score.template.mei` into `sources/score.mei` (filling the
header from the config), fragments the score into tasks, and writes
`tracking/state.csv` (every task `encoding_required`) and an empty
`tracking/locks.csv`. From there, volunteers claim and submit work as pull
requests, which Actions validate and merge while keeping the tables current.

## File formats

`config.yaml` is YAML; `state.csv` and `locks.csv` are CSV (chosen for clean,
cell-level pull-request diffs and trivial machine parsing). The schema, the
column meanings, and the validation-cell encoding are specified in `DESIGN.md`
in the `instigation` repo (the single design + status document for the project).
