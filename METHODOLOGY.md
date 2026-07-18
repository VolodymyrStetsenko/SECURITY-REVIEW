# Research Methodology

Version: `1.0`  
Maintainer: Volodymyr Stetsenko  
Scope: public Web3 incident investigations, security assessments, and defensive labs

## Purpose

This methodology exists to make research reviewable. It separates confirmed evidence from inference, preserves the path from source to conclusion, and prevents a polished narrative from hiding uncertainty.

The process is built around the **Exploit-Chain Framework**:

```text
ASSET
  ↓
TRUST ASSUMPTION
  ↓
PRIVILEGE
  ↓
CONTROL
  ↓
EXTERNAL DEPENDENCY
  ↓
ATTACK PATH
  ↓
ECONOMIC IMPACT
```

## 1. Research question

Every case begins with one falsifiable question. Examples:

- Which security assumption failed first?
- How did privileged access become extractable value?
- Which dependency allowed an apparently valid state transition?
- Which control would have prevented or contained the loss?

A case should not begin with a predetermined conclusion such as “the protocol was hacked because of X.”

## 2. Scope and boundaries

Record before analysis:

- systems, contracts, networks, and time window included;
- systems and claims explicitly excluded;
- whether the work is an incident investigation, assessment, lab, or method;
- whether any private or authorised information is involved;
- publication constraints and responsible-disclosure obligations.

## 3. Evidence hierarchy

Evidence is ranked by directness:

| Level | Evidence | Examples |
|---|---|---|
| `E1` | Primary technical evidence | transaction receipt, event log, verified code, trace, storage state, commit |
| `E2` | Primary first-party statement | protocol post-mortem, official disclosure, maintainer statement |
| `E3` | Reputable secondary analysis | established security researcher or firm with visible methodology |
| `E4` | Unverified secondary reporting | media summary, social post, copied claim |
| `E5` | Independent inference | reasoned conclusion derived from E1–E4 evidence |

A material claim should cite the strongest available level. `E5` conclusions must identify the supporting evidence and be labelled as inference.

## 4. Confidence labels

- **Confirmed** — directly supported by primary evidence.
- **High confidence** — multiple consistent sources, with no material contradiction.
- **Moderate confidence** — plausible and supported, but one or more important gaps remain.
- **Low confidence** — incomplete evidence or significant alternative explanations.
- **Unresolved** — evidence is insufficient to state a conclusion.

Confidence describes the evidence, not the writing quality.

## 5. System and trust model

Before reconstructing the exploit, document:

1. protected asset or invariant;
2. actors and privileged roles;
3. upgrade and emergency paths;
4. external dependencies;
5. expected control at each trust boundary;
6. monitoring and incident-response assumptions.

The objective is to identify what had to remain true for the system to be safe.

## 6. Chronology

Build a timestamped chronology containing:

- transaction or event reference;
- actor or address;
- action;
- asset/state change;
- evidence level;
- confidence;
- interpretation.

Do not merge separate transactions into a single narrative step when the separation matters to causality.

## 7. Exploit-chain reconstruction

The chain should distinguish:

1. **Preparation** — funding, approvals, testing, infrastructure, or reconnaissance visible in public evidence.
2. **Initial access or failure** — compromised privilege, code path, dependency, or operational process.
3. **Control expansion** — role grants, upgrades, parameter changes, signer changes, or state manipulation.
4. **Value creation or distortion** — mint, price distortion, accounting error, or invalid message acceptance.
5. **Economic conversion** — borrow, swap, redeem, bridge, or withdrawal into a real asset.
6. **Exit and aftermath** — routing, recovery, pause, burn, bad debt, or unresolved balances.

A case can omit stages that are not applicable, but it should not invent missing steps.

## 8. Root-cause model

Root cause is separated into layers:

- **Implementation** — local code defect.
- **Protocol logic** — flawed economic or state-transition design.
- **Privilege and lifecycle** — admin, upgrade, governance, deployment, key management.
- **External dependency** — oracle, bridge, signer, RPC, device, verifier, third-party service.
- **Detection and response** — monitoring, pause, communication, recovery.

The report should identify both the initiating failure and the controls that allowed impact to expand.

## 9. Defensive control map

Recommendations are connected to explicit failure points:

| Control type | Examples |
|---|---|
| Preventive | multisig separation, timelock, cap, invariant, allowlist, validation |
| Detective | role-change alert, mint threshold, anomaly detection, reconciliation |
| Containment | pause, borrow cap, isolation mode, withdrawal delay |
| Recovery | key rotation, admin recovery, incident playbook, communication path |

Generic recommendations such as “improve security” are not accepted.

## 10. Defensive lab standard

A lab must state:

- local, historical fork, testnet, or explicitly authorised environment;
- exact setup and dependency versions;
- expected vulnerable behaviour;
- test demonstrating the behaviour;
- defensive variant or control;
- limitations compared with the real incident.

The lab should be reproducible without interacting with live victim systems.

## 11. Assessment standard

A security assessment must identify:

- target commit, files, and lines of code where practical;
- review dates and reviewer;
- methodology and tools;
- trust assumptions and exclusions;
- severity model;
- findings with impact, likelihood, evidence, recommendation, and status;
- explicit limitation that the review does not guarantee absence of vulnerabilities.

## 12. Publication checklist

A case cannot move to `Published` until:

- [ ] scope and exclusions are visible;
- [ ] material claims cite evidence;
- [ ] facts and inference are separated;
- [ ] uncertainty is labelled;
- [ ] exploit-chain diagram or ordered sequence exists;
- [ ] defensive control map exists;
- [ ] sources and access dates are recorded;
- [ ] legal/ethical scope is stated;
- [ ] report links resolve;
- [ ] lab instructions are tested when a lab is included;
- [ ] publication registry is updated.

## 13. Corrections

Material corrections must preserve provenance. The original statement, corrected statement, date, reason, and affected artifacts are recorded under the process in `PUBLICATION_POLICY.md`.
