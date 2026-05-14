# CDAP build.yml label-persistence race PoC

Demonstrates the regression on Google's fix for [M3Pjk25Sn](https://bughunters.google.com/reports/vrp/M3Pjk25Sn/report).

The `.github/workflows/build.yml` is byte-identical to `data-integrations/google-cloud/.github/workflows/build.yml`
EXCEPT for the `runs-on:` line (changed from `k8s-runner-build` to `ubuntu-latest` so we can actually
exercise the workflow without access to Google's self-hosted runner).

The label-persistence race: after a maintainer adds the `build` label, any subsequent `synchronize`
event (push to the PR head) re-runs the workflow on the new SHA without re-review.
// benign change
