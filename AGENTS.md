Security model: [SECURITY.md](./SECURITY.md)

## apache-magpie framework

This repo adopts the
[`apache/magpie`](https://github.com/apache/magpie)
framework via the snapshot mechanism. The framework
provides the `pr-management-*`, `issue-*`, and `security-*`
skills; they are gitignored symlinks into the
`.apache-magpie/` snapshot directory.

A fresh clone needs the snapshot populated before any
framework skill is invocable. Run `/magpie-setup` (or
follow [`.agents/skills/magpie-setup/`](.agents/skills/magpie-setup/))
to fetch it per the committed
[`.apache-magpie.lock`](.apache-magpie.lock). The
contributor-facing summary of the adoption + setup flow
lives in the
[Agent-assisted contribution section of `README.md`](README.md#agent-assisted-contribution-apache-magpie).

Adopter-specific modifications to framework-skill
workflows live in
[`.apache-magpie-overrides/`](.apache-magpie-overrides/)
— never edit the snapshot directly. Framework changes go
via PR to
[`apache/magpie`](https://github.com/apache/magpie).

### Reviewing pull requests

With apache-magpie installed locally, use the
`magpie-pr-management-code-review` skill for PR code
review. It posts findings as **inline review comments**
anchored to `file:line`, presented **individually for
accept/skip** before anything is submitted — prefer it
over an ad-hoc review pass or a generic review command. A
body-only review is the explicit opt-out (`inline:off`).
