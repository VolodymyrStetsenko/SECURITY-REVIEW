# Stetsenko Security Research

**Public evidence library for Web3 security assessments, incident investigations, defensive labs, and research methods.**

This repository is the canonical index of my public security work. It is designed as an evidence system rather than a collection of disconnected PDFs: every publication should state its scope, provenance, confidence, limitations, and relationship to reproducible technical work.

> Videos, posts, and presentations distribute the research. This repository remains the source of record.

---

## Research library

### Security assessments

| ID | Project | Date | Type | Findings | Report | Context |
|---|---|---:|---|---:|---|---|
| `SA-2025-001` | PasswordStore | 2025-11-26 | Portfolio security assessment | 2 High · 1 Informational | [PDF](reports/pdf/2025-11-26_PasswordStore.pdf) | Public portfolio evidence; not represented as a client engagement |
| `SA-2025-002` | RaiseBox Faucet | 2025-12-27 | Portfolio security assessment | 2 High · 1 Medium | [PDF](reports/pdf/2025-12-27_Raisebox_Faucet.pdf) | Public portfolio evidence; not represented as a client engagement |

### Incident investigations

| ID | Case | Network | Status | Canonical artifact | Lab | Video |
|---|---|---|---|---|---|---|
| `IR-2026-001` | Echo Protocol eBTC privileged-access incident | Monad | In progress | Publication pending | Safe local reproduction planned | English video planned |

### Defensive labs

| Lab | Purpose | Repository | Status |
|---|---|---|---|
| SecureVault | Unit, attack-simulation, and invariant-testing workflow | [SecureVault-Foundry](https://github.com/VolodymyrStetsenko/SecureVault-Foundry) | Public; verification refresh scheduled |
| Echo-style privileged-role lab | Demonstrate admin takeover, mint authority, fake collateral, and defensive controls in a safe environment | Publication pending | In progress |

---

## The case-file standard

A complete incident case should answer six questions:

1. **What happened?** — confirmed chronology and affected assets.
2. **What security assumption failed?** — the trust boundary that stopped being true.
3. **What was the exploit chain?** — the ordered path from access or bug to state change and economic impact.
4. **What evidence confirms each step?** — transactions, events, code, public statements, and source quality.
5. **What remains uncertain?** — unresolved claims are labelled rather than presented as facts.
6. **What controls would have prevented or limited the incident?** — architecture, privilege, monitoring, response, and operational controls.

The full process is documented in [METHODOLOGY.md](METHODOLOGY.md).

## Evidence classes

| Class | Purpose | Required minimum |
|---|---|---|
| **Incident case file** | Reconstruct a real exploit or security failure | Scope, timeline, evidence map, exploit chain, uncertainty, control map, sources |
| **Security assessment** | Document a bounded review of code or protocol behaviour | Commit/scope, methodology, findings, limitations, severity rationale |
| **Defensive lab** | Reproduce a known failure safely and test mitigations | Local/fork-only scope, setup, tests, expected results, defensive variant |
| **Method** | Publish a reusable analysis or review framework | Problem definition, process, examples, limitations, version history |

## Finding registry

Current public assessment totals:

| Critical | High | Medium | Low | Informational | Gas |
|---:|---:|---:|---:|---:|---:|
| 0 | 4 | 1 | 0 | 1 | 0 |

Counts are descriptive portfolio metrics, not a substitute for impact, report quality, or independently validated client outcomes.

## Repository architecture

```text
SECURITY-REVIEW/
├── README.md                         # Public index and navigation
├── METHODOLOGY.md                    # Research and evidence standard
├── PUBLICATION_POLICY.md             # Provenance, corrections, and claim policy
├── registry/
│   └── publications.json             # Machine-readable publication ledger
├── templates/
│   ├── CASE_FILE_TEMPLATE.md         # Incident investigation template
│   └── SECURITY_ASSESSMENT_TEMPLATE.md
├── reports/
│   └── pdf/                          # Existing published assessment PDFs
├── cases/
│   └── YYYY-case-name/               # Future canonical incident case folders
│       ├── README.md
│       ├── report/
│       ├── evidence/
│       ├── diagrams/
│       ├── lab/
│       └── media/
└── assessments/
    └── YYYY-project-name/             # Future Markdown + PDF assessment packages
```

Existing reports remain at their current stable paths. New publications should use the structured `cases/` or `assessments/` model.

## Publication states

- `Draft` — private or incomplete research.
- `In progress` — publicly announced work with incomplete evidence or artifacts.
- `Published` — minimum publication standard satisfied.
- `Corrected` — a material correction was issued with a change record.
- `Superseded` — a newer report or method replaces the item.
- `Archived` — retained for provenance but no longer actively maintained.

## Integrity and limitations

- Portfolio assessments are labelled as portfolio work unless a client relationship is explicitly documented and publication is authorised.
- Historical incident research separates confirmed facts, credible secondary reporting, and independent inference.
- Labs are defensive and restricted to owned systems, local environments, public test environments, historical forks, or explicitly authorised work.
- No publication should imply that a review guarantees the absence of vulnerabilities.
- Material corrections are recorded transparently under the policy in [PUBLICATION_POLICY.md](PUBLICATION_POLICY.md).

## Contact and collaboration

For research collaboration, technical writing, incident-analysis support, or bounded protocol-readiness work:

- [GitHub profile](https://github.com/VolodymyrStetsenko)
- [LinkedIn](https://www.linkedin.com/in/volodymyr-stetsenko-656014246/)
- [X](https://x.com/carstetsen)

---

**Independent research · Evidence before claims · Defensive work only**
