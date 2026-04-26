# Verification And Validation Guide

Keep verification and validation separate in every requirement review.

```text
Verification: did we build it right?
Validation: did we build the right thing?
```

## Verification

Verification checks whether the implementation satisfies a requirement.

| Method | Meaning | Use When | Evidence Examples |
|---|---|---|---|
| Inspection | Human or automated review of an artifact | Static properties, document content, config, UI presence | checklist, screenshot, lint result, review note |
| Analysis | Reasoned proof, calculation, model, query, or static analysis | Performance budgets, capacity, coverage, threat reasoning | calculation, report, model output, query result |
| Demonstration | Show behavior without full instrumentation | Workflow behavior, operator procedure, visible system response | demo record, screen capture, manual run result |
| Test | Execute controlled procedure and compare result | Functional behavior, API behavior, regression, performance | automated test, ATP result, test report |

Verification review questions:

- What exact requirement is being verified?
- Which method applies?
- What is the pass/fail or acceptance condition?
- What environment, version, data set, or build is under test?
- Where is the result recorded?
- What happens if the result is partial, failed, or deferred?

## Validation

Validation checks whether the result satisfies the parent need, user outcome, or
operational context.

| Method | Meaning | Evidence Examples |
|---|---|---|
| Stakeholder review | A representative accepts or rejects the result | approval note, review record, signed acceptance |
| User scenario | A representative workflow proves intended use | scenario result, UAT note, task completion evidence |
| Operational dry run | Operational procedure is exercised before production | runbook execution, incident drill, support rehearsal |
| Acceptance test | End-to-end scenario tied to user value | acceptance result, ATP/ATR, demo report |
| Production feedback | Real use confirms intended outcome after release | telemetry, support signal, customer confirmation |

Validation review questions:

- Which need or user outcome is being validated?
- Who is the stakeholder, representative, or approved proxy?
- What scenario represents real use?
- What acceptance signal is sufficient?
- Is validation complete, planned, deferred, or missing?
- If deferred, who owns it and what trigger closes it?

## Verification Does Not Replace Validation

Common mistakes:

- Unit tests verify code paths, but do not automatically validate user value.
- Integration tests verify system interactions, but may not prove operational acceptance.
- A passing build verifies buildability, not requirement satisfaction.
- A demo may support validation, but only if it uses a representative scenario and acceptance signal.
- Stakeholder approval validates intent, but does not prove technical verification.

## Requirement V&V Readiness

For each requirement, require:

| Field | Minimum Standard |
|---|---|
| Verification method | Inspection, analysis, demonstration, or test |
| Verification criteria | Objective pass/fail, threshold, artifact, or review condition |
| Verification owner | Person or role accountable for evidence |
| Validation path | Need, scenario, stakeholder review, operational dry run, acceptance, or approved deferred plan |
| Validation owner | Person or role accountable for acceptance |
| Evidence link | Current result, expected result artifact, ATP entry, or planned evidence |

## Missing V&V Handling

| Gap | Action |
|---|---|
| No verification method | Block approval or require rewrite |
| Method exists but no pass/fail condition | Revise |
| Verification deferred | Require owner, trigger, and accepted risk/gap |
| No validation path for user-facing behavior | Block approval or require explicit deferred validation |
| Validation depends on human judgment | Require named stakeholder/reviewer or approved proxy |
| Unit tests claimed as validation | Downgrade to verification unless scenario validates need |

## ATP And Result Guidance

Use ATP entries for named procedures or scenarios:

```markdown
| ATP ID | Requirement | Method | Setup / Context | Expected Result | Owner | Status |
|---|---|---|---|---|---|---|
```

Use result records for actual evidence:

```markdown
| Result ID | Requirement / Need | ATP / Method | Tested Ref | Outcome | Evidence | Date |
|---|---|---|---|---|---|---|
```

An activity without outcome, context, and tested reference is not evidence.
