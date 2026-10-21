# Standup CI Triage Notes

Morning standup prep — one-page triage of the inbox and the CI picture across repositories.

## Notification Triage

**Inbox could not be read or cleared with the current token.** Every call to the GitHub notifications API (listing unread items, both default and participating views, and marking all as read) was rejected with `403 Resource not accessible by personal access token`. The personal access token in use does not have the notifications scope, so:

- No unread notification items could be enumerated — there is no per-item triage to report from the inbox itself.
- The inbox was **not** marked as read. It must be cleared manually (or with a token granted the `notifications` scope) — inbox zero was not achieved today via automation.

Substitute signal (from repository state instead of the inbox) — items that want attention right now:

- `mcpmark-eval-liuhezi/agent-lab-notes` — PR #11 "Add starred repositories activity report for quarterly team sync" carries a **red** check: its latest CI run failed at the workflow level (see CI status below). This is the one genuinely red pipeline.
- `mcpmark-eval-liuhezi/ci-smoke-demo` — PR #2 "Add CI smoke-test workflow" is open and green; it re-introduces CI that was removed from `main` in the latest commit.
- `mcpmark-eval-liuhezi/ci-hygiene-audit` — PR #2 "Add audit notes" is open and green; docs-only change awaiting review.
- `mcpmark-eval-liuhezi/pipeline-handover` — PR #5 "Add pipeline documentation" is open and green; docs-only change awaiting review.

## CI Status

### Personal repositories (HeziLiu/*)

None of them have any GitHub Actions workflows at all — no workflow runs exist, so there is nothing to report and nothing to re-run:

- `HeziLiu/Little-rookie` — no workflows, no runs
- `HeziLiu/Big-Buzzard` — no workflows, no runs
- `HeziLiu/CodingInterviewChinese2` — no workflows, no runs
- `HeziLiu/awesome-chatgpt-prompts-zh` — no workflows, no runs

### Organization repositories (mcpmark-eval-liuhezi) with Actions activity

Most recent run per repository, with each job's name and outcome:

| Repository | Latest run | Job | Outcome |
| --- | --- | --- | --- |
| `agent-lab-notes` | handoff-check #8 (run 39631250759) | — (no jobs executed) | **FAILED** (workflow-level failure) |
| `ci-smoke-demo` | CI Smoke Test #3 (run 39645858443) | Smoke check | PASSED |
| `ci-hygiene-audit` | Hygiene Audit #3 (run 39646842536) | hygiene | PASSED |
| `pipeline-handover` | Build #3 (run 39646613791) | build | PASSED |
| `ci-artifact-audit` | artifact-demo #1 (run 39643426179) | build | PASSED |
| `hygiene-rehearsal` | Rehearsal Audit #7 (run 39642366615) | audit | PASSED |
| `ci-cancel-drill` | Long Run #7 (run 39643066671) | sleep-job | PASSED |
| `oncall-drill-2026` | stuck-job #2 (run 39640159017) | stuck-job | CANCELLED (deliberate drill cancellation — not a failure) |
| `ci-drill-sandbox-3` | Idle Drill #1 (run 39251413929) | idle | CANCELLED (deliberate drill cancellation — not a failure) |
| `drill-ci-rehearsal` | CI Drill Hold #1 (run 39542728758) | hold | CANCELLED (deliberate drill cancellation — not a failure) |
| `ci-smoke-template` | Smoke Test #1 (run 39233889913) | smoke | PASSED |
| `release-drill-lab` | CI #1 (run 39227935434) | build | PASSED |
| `github-automation-audit` | Audit evidence #3 (run 39308587706) | upload-evidence | PASSED |
| `heziliu-pr-review-walkthrough` | CI #1 (run 35409482531) | verify | PASSED |
| `handover-pack` | Runbook Validation #4 (run 39457586061) | Validate runbook | PASSED |
| `ci-runbook-drill-2` | Runbook drill | — | workflow defined but no runs yet |

All remaining organization repositories have no workflows and therefore no runs. Three repositories show `cancelled` conclusions on their latest run; each is a deliberate drill cancellation (runaway-job / stuck-job rehearsals), not a flaky failure, so they were not re-triggered.

## Re-runs

- **`agent-lab-notes`, run 39631250759 (handoff-check #8) — FAILED.** A re-run of just the failed jobs was attempted and GitHub refused it with `403 This workflow run cannot be retried`. The run failed before any job started (zero jobs recorded), so there is nothing job-scoped to retry — the workflow definition itself on the `stars-activity-report` branch (PR #11) likely needs to be fixed first.
- No other repository's most recent run had failed jobs, so no other re-runs were triggered.
