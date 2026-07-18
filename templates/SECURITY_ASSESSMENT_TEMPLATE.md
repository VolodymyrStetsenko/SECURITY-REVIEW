# `[SA-YYYY-NNN] Project security assessment`

**Status:** Draft  
**Reviewer:** Volodymyr Stetsenko  
**Review dates:** YYYY-MM-DD — YYYY-MM-DD  
**Target repository:**  
**Target commit:**  
**Assessment context:** Portfolio / contest / client-authorised  
**Languages / frameworks:**  

## Executive summary

Summarise the scope, most important risks, and overall limitation of the review. Do not present finding counts as a guarantee of security.

## Scope

### Reviewed

- Contracts / files:
- Commit or release:
- Lines of code where practical:
- Deployment or configuration assumptions:

### Excluded

- 

## Methodology

- Manual code review
- Architecture and trust-boundary review
- Access-control and privilege analysis
- State-transition and invariant analysis
- Unit, fuzz, invariant, or attack-simulation testing where applicable
- Static analysis and compiler/tooling review where applicable

List exact tool versions and commands when they materially support a claim.

## Trust assumptions

| Assumption | Owner / component | Failure impact |
|---|---|---|
|  |  |  |

## Severity model

Severity is based on impact, likelihood, exploit preconditions, affected assets, and recoverability. A report should explain deviations from the selected severity framework.

| Severity | General meaning |
|---|---|
| Critical | Direct or systemic loss with realistic exploitation and limited recovery |
| High | Major loss, privilege abuse, or invariant failure under credible conditions |
| Medium | Meaningful security or availability impact requiring specific conditions |
| Low | Limited impact or defensive-hardening issue |
| Informational | Clarity, maintainability, monitoring, or best-practice observation |

## Findings summary

| ID | Severity | Title | Status |
|---|---|---|---|
|  |  |  | Open |

## Finding template

### `[H-01] Finding title`

**Severity:** High  
**Status:** Open  
**Affected component:**  
**Evidence:** file, function, line, test, trace, or command

#### Description

#### Impact

#### Preconditions and likelihood

#### Evidence or reproduction

#### Recommendation

#### Resolution status

## Positive observations

Record meaningful controls or design decisions that reduce risk. Avoid generic praise.

## Limitations

- The assessment is limited to the stated scope, commit, dates, and assumptions.
- It does not guarantee that all vulnerabilities or operational risks have been identified.
- Code or configuration changes after the reviewed commit may invalidate conclusions.
- Production security also depends on deployment, keys, monitoring, governance, and external dependencies.

## Reproducibility

```bash
# Build

# Test

# Static analysis

# Coverage / invariant commands
```

## Change history

| Version | Date | Change |
|---|---:|---|
| 1.0 | YYYY-MM-DD | Initial publication |
