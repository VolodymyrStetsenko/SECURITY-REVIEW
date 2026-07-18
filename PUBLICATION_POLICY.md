# Publication, Provenance, and Correction Policy

Version: `1.0`

## 1. Objective

Public security research should be useful, reviewable, and honest about its limits. This policy defines how work is labelled, sourced, corrected, and separated from client or employment claims.

## 2. Work labels

Every publication must use one of these context labels:

- **Independent incident research** — analysis based on public evidence.
- **Portfolio security assessment** — practice or portfolio review, not a paid client engagement unless explicitly stated.
- **Client-authorised assessment** — published only with documented permission.
- **Contest or bounty submission** — identifies the platform, rules, and outcome where disclosure is allowed.
- **Defensive lab** — local, fork-based, testnet, or explicitly authorised reproduction.
- **Method or educational note** — reusable research process or technical explanation.

A publication must not imply a client relationship, award, certification, or production deployment that cannot be independently supported.

## 3. Source provenance

Each report should preserve:

- source title or system;
- canonical URL, transaction hash, contract address, commit, or document identifier;
- access date;
- relevant archive or snapshot when practical;
- evidence level and confidence for material claims.

Screenshots may illustrate evidence but do not replace canonical references.

## 4. Facts, reporting, and inference

Reports distinguish:

- **Confirmed fact** — primary technical or first-party evidence.
- **Reported claim** — attributed to a named source.
- **Independent inference** — the researcher's conclusion, with supporting evidence.
- **Unresolved question** — evidence is insufficient or contradictory.

Headlines and summaries must not remove these distinctions.

## 5. Corrections

A correction is material when it changes:

- the identified root cause;
- affected amount, asset, address, or transaction;
- severity or finding validity;
- attribution;
- exploit-chain sequence;
- a recommendation that could materially affect a reader's decision.

For a material correction:

1. update the canonical report;
2. add a dated correction note near the affected claim;
3. record the change in a `CHANGELOG.md` inside the case or assessment folder;
4. update linked diagrams, labs, videos, and the publication registry;
5. preserve the previous Git history rather than silently rewriting provenance.

Minor spelling or formatting fixes do not require a correction notice.

## 6. Publication status

- `Draft` — incomplete and not intended as a stable reference.
- `In progress` — public work with missing evidence or artifacts.
- `Published` — minimum methodology and publication checklist satisfied.
- `Corrected` — at least one material correction has been issued.
- `Superseded` — a later publication replaces the work.
- `Archived` — retained for provenance but no longer maintained.

## 7. Security and ethical boundary

Technical demonstrations are restricted to:

- owned systems;
- local environments;
- public test networks;
- historical fork analysis;
- explicitly authorised assessments or programs.

The repository is intended for defensive research, education, risk reduction, and responsible disclosure. It is not an invitation to interact with live systems without permission.

## 8. Confidentiality

Confidential client information, private keys, personal data, credentials, and unpublished vulnerability details are not committed to this repository. Sanitised case studies require permission and must remove information that could expose a client or unresolved vulnerability.

## 9. External review and feedback

Corrections, source disputes, and technical review are welcome through a GitHub issue or direct contact. A disagreement is not automatically treated as a correction; the evidence is reviewed against the methodology before publication status changes.

## 10. Limitations

A security assessment is time-bound and scope-bound. It cannot guarantee that all vulnerabilities, operational risks, or future changes have been identified. Incident research may remain incomplete when evidence is private, unavailable, or technically ambiguous.
