<!-- SPDX-License-Identifier: Apache-2.0
     https://www.apache.org/licenses/LICENSE-2.0 -->

# Apache JMeter — project manifest

Project configuration for **Apache JMeter**. Every apache-magpie
framework skill reads this manifest to resolve project-specific
identity, repositories, mailing lists, and workflow knobs. Values not
declared here fall back through the resolution chain
`project.md → organizations/ASF/organization.md → framework default`.

Grep for `TODO` to see fields that still need a human decision:

```bash
grep -n TODO .apache-magpie-overrides/project.md
```

> **Scope note.** JMeter runs **no dedicated GitHub security-tracker
> repo and no Projects V2 board** (`.asf.yaml` sets `projects: false`).
> Vulnerabilities are reported to the ASF-wide `security@apache.org`
> and discussed on `private@jmeter.apache.org`; CVEs go through the ASF
> CVE process. Consequently the security-*tracker* skills
> (`security-issue-import`, `security-issue-triage`,
> `security-issue-sync`, `security-tracker-stats-dashboard`, board
> reconciliation, issue-template fields) have **no tracker to operate
> on** until/unless the PMC stands one up — those blocks below are
> marked *N/A*. The mail-reading and CVE-allocation paths still work
> against the mailing lists and the ASF CVE tooling.

## Identity

| Key | Value |
|---|---|
| `organization` | `ASF` |
| `project_name` | `Apache JMeter` |
| `vendor` | `Apache Software Foundation` |
| `short_name` | `JMeter` |
| `product_family_url` | `https://jmeter.apache.org/` |

## Repositories

| Key | Value | Purpose |
|---|---|---|
| `tracker_repo` | *N/A — no dedicated GitHub security tracker* | Would be the private security tracker repo |
| `tracker_repo_url` | *N/A* | |
| `tracker_default_branch` | *N/A* | |
| `tracker_project_board_url` | *N/A — `.asf.yaml` `projects: false`* | |
| `issue_tracker_repo` | `apache/jmeter` | General issue tracker = GitHub Issues on the codebase repo (used by the `issue-*` skills) |
| `upstream_repo` | `apache/jmeter` | Public codebase where fixes land |
| `upstream_repo_url` | `https://github.com/apache/jmeter` | |
| `upstream_default_branch` | `master` | What `<default-branch>` resolves to |
| `upstream_agents_md_url` | TODO — `AGENTS.md` not yet on `apache/jmeter@master` (present only on this branch); set once upstreamed | Conventions this repo mirrors |
| `upstream_contributing_docs_url` | `https://github.com/apache/jmeter/blob/master/CONTRIBUTING.md` | |
| `upstream_genai_disclosure_anchor` | TODO — link to JMeter's Gen-AI contribution guideline if/when published | |
| `upstream_security_policy_url` | `https://github.com/apache/jmeter/security/policy` | |

## Mailing lists

| Key | Value | Notes |
|---|---|---|
| `security_list` | `security@apache.org` | JMeter has **no** project-specific `security@jmeter`; reports go to the ASF-wide address (per `SECURITY.md`) |
| `private_list` | `private@jmeter.apache.org` | PMC-private; where security discussion lands. Read via PonyMail (allow-listed) |
| `users_list` | `user@jmeter.apache.org` | Public; note the **singular** local part |
| `dev_list` | `dev@jmeter.apache.org` | Release `[RESULT][VOTE]` threads; also the `.asf.yaml` issues/PR notification target |
| `announce_list` | `announce@apache.org` | Foundation-wide announce (JMeter has no project-specific announce list archived on PonyMail) |
| `commits_list` | `commits@jmeter.apache.org` | Publicly archived |
| `asf_security_list` | `security@apache.org` | ASF security team; the inbound path for JMeter |

Public archives: `https://lists.apache.org/list.html?<list>`.
`private@jmeter.apache.org` is member-only (PonyMail LDAP session).

## Tools enabled

| Capability | Tool | Config knobs |
|---|---|---|
| Issue tracking (general) | `github` | `issue_tracker_repo = apache/jmeter` (GitHub Issues enabled; no Projects board) |
| Source control (VCS) | `github` (Git) | `upstream_repo = apache/jmeter`, `upstream_default_branch = master` |
| Inbound email / drafts | `gmail` (primary, write) + `ponymail` (read, ASF archive) | see [Mail sources](#mail-sources) |
| CVE allocation | `vulnogram` (ASF-hosted) | org-level ASF defaults; see below |
| ASF project metadata | `apache-projects` | inherited ASF default (`mandatory: true`) — MCP registered |
| Release voting / announce | ASF mailing lists | via `dev_list` / `announce_list` / `users_list` |

## CVE tooling

ASF project → CNA is the **ASF Vulnogram** process. The tool URLs
(`cve_tool_allocate_url`, `cve_tool_record_url_template`, state
mapping) are **org-level**, inherited from
`organizations/ASF/organization.md`. Only the project-specific CNA
identifiers are declared here:

| Key | Value |
|---|---|
| `cve_tool` | `vulnogram` (ASF-hosted) |
| `asf_org_id` | `f0158376-9dc2-43b6-827c-5f631a4d8d09` (ASF CNA org UUID) |
| `cna_private_owner` | `jmeter` |
| `cna_private_projecturl` | `https://jmeter.apache.org/` |
| `cna_private_userslist` | `user@jmeter.apache.org` |
| `cve_allocation_gated_by` | `Apache JMeter PMC membership (ASF OAuth)` |

## GitHub project board

*N/A.* `.asf.yaml` sets `projects: false`; JMeter runs no security
Projects V2 board. Skills treat missing board config as "no board
reconciliation".

## Mail sources

### Backend declaration

| Backend | Role | Mandatory | Notes |
|---|---|---|---|
| `gmail` | `primary` | `no` | Draft composition + inbound reads from a subscribed Gmail account. Only write-capable backend. |
| `ponymail` | `preferred for archive reads` | `yes` (ASF default) | Read-only ASF archive; PMC LDAP session (cookie) required for `private@jmeter.apache.org`. Registered + allow-listed. |

> Per the ASF default, `ponymail` is `mandatory: yes` — the
> mail-reading skills refuse to run without it. Gmail keeps the
> `primary` role because PonyMail is read-only (drafts stay on Gmail).

### Per-backend config

| Key | Backend | Value |
|---|---|---|
| `security_list_domain` | `gmail` | *N/A — reports arrive at `security@apache.org`, not a `security.jmeter.apache.org` domain* |
| `ponymail_thread_url_template` | `ponymail` | `https://lists.apache.org/thread/<hash>?<list>` |
| `ponymail_allowed_lists` | `ponymail` | `private@jmeter.apache.org` (the `PONYMAIL_ALLOWED_LISTS` value the MCP is registered with) |

## Issue-template fields

*N/A for the security tracker* (no GitHub security tracker repo /
issue template). The general `apache/jmeter` GitHub Issues use the
project's standard bug/feature templates; the `issue-*` skills read
issue bodies free-form and do not depend on this mapping.

## Security workflow configuration

Resolution chain: `project.md → organizations/ASF/organization.md →
framework default`. ASF org defaults supply the CNA tool, governance
gate, mail/forwarder/archive backends, and roster lookup. Only
project-specific overrides are declared below.

### CVE authority

Org-level — inherited from `organizations/ASF/organization.md`
(Vulnogram CNA, allocate/record URLs, state mapping). No project
override.

### Governance

Org-level except the escalation contact:

```yaml
governance:
  # PMC/security escalation contact for @-mentions beyond the security team.
  escalation_contact: "TODO: @<jmeter-pmc-security-contact>"
```

### Security inbox

```yaml
security_inbox:
  # JMeter's inbound security address is the ASF-wide team address.
  address: security@apache.org
```

### Forwarders

Org-level (ASF security-team relay). JMeter reports commonly arrive
**relayed** from the ASF security team onto `private@jmeter`, so the
ASF forwarder adapter applies. No extra project relay.

### Mail provider / Archive system / Project metadata

Org-level — inherited from `organizations/ASF/organization.md`
(Gmail+PonyMail; `lists.apache.org` archive; `apache-projects-mcp`).
No project override.

### Tracker

*N/A* — no GitHub security tracker. Skills that reconcile tracker
labels/board are inert for JMeter until a tracker is created.

### Release process

```yaml
release_process:
  stale_milestones: []          # TODO: fill if the PMC tracks overdue milestones
  newsfragments:
    enabled: false              # JMeter maintains a hand-edited changelog, not fragment files
```

### Roster

```yaml
roster:
  # Bare first-name -> GitHub handle, for @-mentions from list threads.
  bare_name_handles:
    "Bruno": "@milamberspace"   # Bruno Demion (Milamber), PMC
    # TODO: add other active JMeter committers/PMC as needed
  # Release managers, current first. TODO: confirm current RM roster.
  release_managers:
    - "TODO: @<current-release-manager>"
```

### Product

```yaml
product:
  name: JMeter
  # Primary Maven artifact.
  package_name: "org.apache.jmeter:ApacheJMeter"
  # Backstop regex to confirm an upstream PR touches the product.
  code_pointer_path_prefix: "src/"
  # Subject prefixes stripped when normalising a CVE title.
  subject_prefix_strip:
    - "[SECURITY]"
    - "[Security Report]"
    - "Re:"
    - "Fwd:"
    - "Apache JMeter:"
    - "JMeter:"
  affected_version_extract_prefix: "JMeter"
```

## Pointers to sibling files

Not yet created — add under `.apache-magpie-overrides/` only if a
skill asks for one:

- `release-trains.md` — release state + RM attribution
- `security-model.md` — Security-Model URL + anchors (JMeter: see `THREAT_MODEL.md`)
- `fix-workflow.md` — fork / toolchain / commit-trailer specifics
- `canned-responses.md` — reporter-facing reply templates
