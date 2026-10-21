# Smoke Test Demo Notes

This repository is a throwaway sandbox for demoing GitHub Actions end-to-end in a
workshop. The `.github/workflows/smoke.yml` workflow is picked up automatically and,
on every `push` and `pull_request` event, runs a job on an `ubuntu-latest` hosted
runner that checks out the repository and executes `scripts/smoke.sh`.

The script prints a one-line greeting and then `uname -a`, so the runner's operating
system is visible right in the job log — a quick way to prove to the audience that the
code is genuinely executing on GitHub's hosted infrastructure.

## How to re-trigger the demo

- **Push a commit:** any new commit pushed to any branch starts a run (trigger: `push`).
  `git commit --allow-empty -m "re-run demo" && git push` is enough.
- **Open or update a PR:** creating a pull request, or pushing new commits to an open
  one, starts a run with the `pull_request` trigger.
- **Re-run from the UI:** on any past run under the **Actions** tab, use
  **Re-run all jobs** to replay the exact same pipeline.

No secrets, no external dependencies, no build tooling — delete the repository when
the workshop is over.
