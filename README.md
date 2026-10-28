# baseliner-control

Runs [baseliner](https://github.com/baselinerhq/baseliner) compliance scans
across the `anolishq` organization. Both workflows pin the same baseliner
release.

- [`baseliner.yaml`](baseliner.yaml) is the org policy: the `default` base
  policy, with this repo excluded and one waiver for
  `anolishq/renovate-config`.
- [`.github/workflows/baseliner.yml`](.github/workflows/baseliner.yml) scans
  every Monday at 06:00 UTC, and on manual `workflow_dispatch`. It uploads
  `results.json` as the `baseliner-results` artifact.
- [`.github/workflows/ci.yml`](.github/workflows/ci.yml) checks that
  `baseliner.yaml` resolves with `baseliner policy`.

## Findings

The scan runs with `--open-issues`, so findings go to a findings issue in each
scanned repo. baseliner closes the issue when the repo is compliant.

The scan also runs with `--fail-under 0 --min-coverage 1.0`. Findings do not
fail the run. A red run means the scan broke, a repo's evidence could not be
read, or a findings issue could not be written. See
[Control Repo](https://baselinerhq.github.io/control-repo).

## Setup

Add a repository secret `BASELINER_TOKEN`: a fine-grained PAT with resource
owner `anolishq`, access to all repositories, and these repository
permissions:

- Metadata: Read
- Contents: Read
- Issues: Read and write

Then run the workflow from the Actions tab.
