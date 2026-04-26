# Systems Engineering Traceability Operating Model

This is an original, lightweight operating model for agentic software development.

It is aligned with systems-engineering concepts from ISO/IEC/IEEE 15288, the INCOSE Systems Engineering Handbook, ISO/IEC/IEEE 29148, ISO/IEC/IEEE 15289, and public NASA systems engineering material, but it does not reproduce those standards or handbooks.

Until reviewed against licensed ground-truth sources, treat this file as project-specific guidance for agent workflows, not as a standards-compliance claim.

## Lifecycle Chain

Preserve traceability through this chain:

```text
intent
  -> stakeholder need
  -> user requirement
  -> system requirement
  -> design decision
  -> implementation
  -> verification
  -> validation
  -> change control
```

For projects that keep separate artifacts, preserve document traceability through:

```text
requirements document
  -> plan document
  -> traceability matrix
  -> acceptance test plan or procedure
  -> result record
```

## Core Agent Rules

1. Brainstorming creates candidate needs, assumptions, risks, and success signals. It does not create implementation authority.

2. Planning converts approved or candidate needs into requirements, design decisions, ATP or result expectations, verification paths, and validation paths.

3. Work agents may only implement meaningful behavior when it traces to approved authority.

4. Review findings are provenance, not authority. They become authority only when converted into an approved requirement change, approved design decision, first-class approved risk control, or approved gap.

5. Requirements may evolve, but they must evolve through explicit change control.

6. A task ID alone is not authority. A task only carries authority when it closes directly to approved upstream authority.

7. A bare `RISK-*` ID is not authority. A risk control only authorizes implementation when it is approved, owned, evidenced, and linked to a requirement or approved gap.

8. Verification asks whether the team built the thing right.

9. Validation asks whether the team built the right thing.

10. Missing traceability must be exposed, not invented.

## Valid Authority

Meaningful implementation behavior must link to at least one valid approved authority:

- approved requirement
- approved ADR or design decision
- first-class approved risk control
- approved traceability gap
- task that closes directly to one of the approved authorities above

The following are not authority by themselves:

- brainstorm ideas
- assumptions
- review findings
- implementation tasks
- inferred links
- draft requirements
- bare `RISK-*` references
- test existence without a requirement or design link

If the authority is inferred, mark it `Draft` and ask for human approval before treating it as implementation authority.

## Traceability Matrix

The Markdown traceability matrix is the audit/control surface for the workflow. It records links, status, owners, evidence references, gaps, and human decisions.

Lite mode may use a minimal matrix row, but it must not skip the matrix artifact entirely when the traceability skill is used. Standard and Audit modes should use the full matrix structure from `references/traceability-matrix-template.md`.

Source artifacts remain authoritative for their own detailed content:

- requirements live in specifications or requirements documents
- design rationale lives in ADRs or design notes
- procedures live in ATPs or test plans
- measured outcomes live in result records

The matrix connects those artifacts. It should not rewrite or replace them.

## Change Control

When requirements, design decisions, risks, validation paths, or meaningful behavior change, update the traceability record in the same work cycle.

If a review finding introduces new scope, convert it into one of:

- requirement change
- design decision
- first-class approved risk control
- approved traceability gap
- rejected finding with rationale

Do not silently promote a review comment, assumption, or inferred link into authority.

## Brownfield Work

For existing projects that did not start with traceability, do not invent historical trace links after the fact.

Record known gaps as traceability debt. Apply strict no-orphan enforcement to new or changed meaningful behavior from the chosen baseline forward. Existing untraced behavior becomes trace-relevant when new work depends on it, modifies it, uses it as authority, or needs it for validation.

## Reference Basis

This operating model is an original, lightweight distillation for agentic software development. It does not reproduce ISO, IEEE, INCOSE, or NASA copyrighted material.

It is informed by the following official or public sources:

| Source | Link | How it is used |
|---|---|---|
| ISO/IEC/IEEE 15288:2023 - Systems and software engineering - System life cycle processes | https://www.iso.org/standard/81702.html | Primary lifecycle-process reference. Used for high-level alignment only. |
| IEEE/ISO/IEC 15288-2023 page | https://standards.ieee.org/ieee/15288/10424/ | Alternate official standards entry point. |
| INCOSE Systems Engineering Handbook, 5th Edition | https://www.incose.org/resources-publications/technical-publications/se-handbook/ | Systems engineering handbook reference aligned with ISO/IEC/IEEE 15288:2023. |
| INCOSE Systems Engineering Standards page | https://www.incose.org/about-systems-engineering/standards-policies/ | Source list for related SE standards such as 15288 and 15289. |
| ISO/IEC/IEEE 29148:2018 - Requirements engineering | https://www.iso.org/standard/72089.html | Requirements engineering reference. |
| IEEE/ISO/IEC 29148 page | https://standards.ieee.org/ieee/29148/12262 | Alternate official requirements-engineering source entry. |
| NASA Requirements Verification Matrix appendix | https://www.nasa.gov/reference/appendix-d-requirements-verification-matrix/ | Public practical example for requirement IDs and verification methods. |
| NASA Systems Engineering Handbook material | https://www.nasa.gov/reference/system-engineering-handbook-appendix/ | Public practical examples for V&V, traceability, and lifecycle evidence. |
