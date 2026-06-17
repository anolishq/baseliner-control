# baseliner-control

Scheduled [baseliner](https://github.com/baselinerhq/baseliner) compliance scans
for the `anolishq` organization.

- [`baseliner.yaml`](baseliner.yaml) — the calibrated org policy (one documented,
  not-applicable waiver).
- [`.github/workflows/baseliner.yml`](.github/workflows/baseliner.yml) — weekly
  scan + manual `workflow_dispatch`; uploads `results.json` as an artifact.

## Setup

Add a repository secret **`BASELINER_TOKEN`** — a fine-grained PAT with resource
owner `anolishq`, **All repositories**, **Contents: read** + **Metadata: read**
(add **Issues: write** only if you enable `--open-issues`). Then run from the
**Actions** tab.

## Steady state

The org is currently fully compliant (13/13 @ 1.00). To turn this into a live
monitor that opens an issue when a repo drifts and closes it when fixed, add
`--open-issues` to the scan step — with baseliner **v0.1.1** that is noise-free
(issues open only on findings).
