<!-- SPDX-License-Identifier: Apache-2.0
     https://www.apache.org/licenses/LICENSE-2.0 -->

# Apache JMeter — pr-management-triage CI-check to doc-URL map

Maps a failing GitHub Actions check to a doc URL for the triage
violations feedback.

**Deliberately generic — no per-check-name patterns.** JMeter's CI matrix
job names are generated dynamically (`matrix.mjs` → `JDK, vendor, os,
timezone, locale` cells) and change often, so any hand-maintained
check-name → category map would go stale quickly. Per the review feedback
on the adoption PR, *stale context is worse than no context*: we keep a
single generic pointer rather than a matrix of names to maintain. All build,
static-check, and test failures are documented in one place — `gradle.md`.

## Table

| Pattern | Category | Doc URL |
|---|---|---|
| `*` (catch-all) | Failing CI check | `https://github.com/apache/jmeter/blob/master/gradle.md` |

## Notes

- **Merge-conflict fallback.** When `mergeable == CONFLICTING`, the skill
  emits a separate "Merge conflicts" category:

| Concept | Doc URL |
|---|---|
| Merge conflicts (rebase guide) | `https://github.com/apache/jmeter/blob/master/CONTRIBUTING.md` |

- **Failing-CI fallback.** If `checks_state == FAILURE` with no extractable
  failed-check names, the skill emits a generic "Failing CI checks" entry
  pointing at the catch-all URL above.
- JMeter has **no** Helm / Kubernetes / provider-testing / image-build CI
  categories — those framework rows are intentionally omitted.
