<!-- SPDX-License-Identifier: Apache-2.0
     https://www.apache.org/licenses/LICENSE-2.0 -->

# Apache JMeter — pr-management-triage configuration

Per-project configuration for the
[`pr-management-triage`](../.apache-magpie/skills/pr-management-triage/SKILL.md)
skill (and the shared bits `pr-management-stats` reads).

## Identifiers

| Key | Value | Notes |
|---|---|---|
| `committers_team` | `apache/jmeter-committers` | ASF committer team for maintainer-to-maintainer mention detection (row F5b). **Verify** the exact team slug in the apache GitHub org before relying on the ping-detection filter. |
| `area_label_prefix` | *(blank)* | JMeter does **not** use `area:*` labels, so PR area-grouping is disabled. The closest dimensions are the type labels (`enhancement`, `defect`, `documentation`, `dependencies`, `tests`) and `os:*` — not an area taxonomy. Leave blank. |

## Project-specific labels

⚠️ **None of the framework's workflow labels exist on `apache/jmeter` yet.**
Creating them is a PMC decision (JMeter keeps a deliberately small label
set). Until they are created, the mapped actions **degrade to
feedback-only** (the skill posts/folds the feedback and skips the label).

| Concept | Value | Status |
|---|---|---|
| `ready_for_maintainer_review` | `ready for maintainer review` | **Not yet created.** Core to `mark-ready` and the `pr-management-code-review` default queue. Create on the repo if the PMC adopts the two-stage flow, else leave the skill in feedback-only mode. |
| `quality_violations_close` | *(blank)* | JMeter has no dedicated label; it uses `wontfix` / `invalid` on close. Leave blank — the `close` action posts its reason without a special label. |
| `suspicious_changes` | *(blank)* | Not used. First-time-contributor workflow-approval flagging degrades to a comment only. |
| `work_in_progress` | *(blank)* | JMeter relies on draft status, not a WIP label. |

## Grace windows

**Tuned longer than the framework defaults** because JMeter triages
infrequently and PRs routinely sit for months (60% of the open backlog is
>1 year old). Short windows would fire stale-action proposals on PRs no
maintainer has had a chance to look at. Revisit once a regular triage
cadence exists.

| Concept | Framework default | JMeter value |
|---|---|---|
| Stale-draft close threshold (triaged) | 7 days | **14 days** |
| Stale-draft close threshold (untriaged) | 14 days | **30 days** |
| Inactive-open → draft threshold | 28 days | **90 days** |
| Stale-review-ping cooldown | 7 days | **14 days** |
| Stale-workflow-approval threshold | 28 days | **90 days** |
| Stale-Copilot-review threshold | 7 days | **14 days** |

## Workflow choices

| Key | Value | Notes |
|---|---|---|
| `triage_feedback_channel` | `pr-body` | Default (quiet): violation feedback is folded into the PR description, not posted as a comment — keeps maintainer mailboxes quiet. Good fit for JMeter's first cleanup pass. |
| `confirmation_handback_mode` | `reviewer-ping` | Framework default. Switch to `maintainer-sweep` only once JMeter runs a regular triage cadence with the `ready for maintainer review` label live. |
| `session_history_gist` | `enabled` | Milamber's token carries `gist` scope; per-session calibration history is proposed (confirm-before-mutate) into a private gist. |
