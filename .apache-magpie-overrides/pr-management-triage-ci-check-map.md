<!-- SPDX-License-Identifier: Apache-2.0
     https://www.apache.org/licenses/LICENSE-2.0 -->

# Apache JMeter — pr-management-triage CI-check to doc-URL map

Maps `apache/jmeter`'s real GitHub Actions check names (case-insensitive
substring match, first-found wins) to a category + doc URL for the triage
violations feedback. Check names were read from live open-PR status
rollups.

## Table

JMeter's CI (Gradle-based) emits: a `Validation` job (Autostyle / Checkstyle
/ SpotBugs / license / build sanity), an `Error Prone (JDK <n>)` static-
analysis job, a `Matrix Preparation` setup job, and a large cross-platform
**test matrix** whose job names encode `JDK, vendor, os, timezone, locale`
(e.g. `21, temurin, macos, UTC, tr_TR`, optionally `… , stress JIT`). The
vendor substrings below catch the matrix rows.

| Pattern | Category | Doc URL |
|---|---|---|
| `validation` | Validation (Autostyle / Checkstyle / SpotBugs / license) | `https://github.com/apache/jmeter/blob/master/gradle.md` |
| `error prone` | Error Prone (static analysis) | `https://github.com/apache/jmeter/blob/master/gradle.md` |
| `matrix preparation` | CI matrix setup | `https://github.com/apache/jmeter/blob/master/gradle.md` |
| `stress jit` | Test matrix (stress-JIT run) | `https://github.com/apache/jmeter/blob/master/gradle.md` |
| `temurin`, `corretto`, `zulu`, `liberica`, `microsoft`, `oracle` | Cross-platform tests (JDK × vendor × OS × locale matrix) | `https://github.com/apache/jmeter/blob/master/gradle.md` |
| `same hashcode` | Test matrix (same-hashcode run) | `https://github.com/apache/jmeter/blob/master/gradle.md` |
| `*` (catch-all) | Other failing CI checks | `https://github.com/apache/jmeter/blob/master/gradle.md` |

## Notes

- **Order matters** — specific rows above the catch-all; the skill matches
  first-found. The vendor row deliberately sits below `validation` /
  `error prone` so those static jobs are categorised distinctly rather than
  as generic tests.
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
