<!-- SPDX-License-Identifier: Apache-2.0
     https://www.apache.org/licenses/LICENSE-2.0 -->

# Apache JMeter — pr-management-triage comment templates

Per-project comment-body values for the
[`pr-management-triage`](../.apache-magpie/skills/pr-management-triage/SKILL.md)
skill. Supplies JMeter's URLs / wording; the framework renders its default
bodies with these. Do **not** duplicate framework default bodies here.

## Project-specific URLs

JMeter has no dedicated "PR quality criteria" or "two-stage triage" pages
(unlike Airflow, whose templates these placeholders were shaped for), so
these point at JMeter's existing contributor docs. The build/test docs are
`gradle.md` and the project site.

| Placeholder | JMeter value |
|---|---|
| `<quality_criteria_url>` | `https://github.com/apache/jmeter/blob/master/CONTRIBUTING.md` |
| `<two_stage_triage_rationale_url>` | `https://magpie.apache.org/` — interim: explains why the first pass is automated. **TODO:** replace with a JMeter-hosted note if the PMC wants project-local wording. |
| `<project_display_name>` | `Apache JMeter` |
| `<merge_conflicts_rebase_url>` | `https://github.com/apache/jmeter/blob/master/CONTRIBUTING.md` |
| `<static_checks_url>` | `https://github.com/apache/jmeter/blob/master/gradle.md` |
| `<testing_url>` | `https://github.com/apache/jmeter/blob/master/gradle.md` |
| `<docs_building_url>` | `https://jmeter.apache.org/building.html` |
| `<project_communication_channel>` | `the JMeter dev mailing list` |
| `<project_communication_url>` | `https://jmeter.apache.org/mail2.html` |

Helm / k8s / provider-testing rows are dropped — JMeter's CI has no such
categories (see the CI-check map).

## Quality-criteria marker string

Framework-fixed — **do not paraphrase**. Must match verbatim what
`pr-management-stats` scans for.

| Concept | Value |
|---|---|
| Triage-marker visible link text | `Pull Request quality criteria` |
| Body-fold block marker tokens (framework-fixed) | `pr-triage-fold` / `/pr-triage-fold` |

## AI-attribution footer

Wording kept close to the framework default; `<PROJECT>` = Apache JMeter,
rationale link as above. Structure (italic meta-block + two-stage-triage
link) preserved.

```markdown
---

_Note: This comment was drafted by an AI-assisted triage tool and may contain mistakes. Once you have addressed the points above, an Apache JMeter maintainer — a real person — will take the next look at your PR. We use this [two-stage triage process](https://magpie.apache.org/) so that our maintainers' limited time is spent where it matters most: the conversation with you._
```

## Template body overrides

None. JMeter uses the framework default bodies rendered with the URLs
above. Add a `### <template-name>` subsection here only if a specific body
must diverge — keep all framework-required marker strings if you do.
