---
name: requirements-reviewer
description: Reviews requirement quality and approval readiness for planning, specs, PRDs, traceability matrices, acceptance criteria, and document reviews. Use when deciding whether a need, requirement, user story, constraint, or acceptance criterion is good enough to become approved implementation authority, or when requirements need classification, rewrite guidance, verification/validation mapping, or structured quality findings.
---

# Requirements Reviewer

## Overview

Judge whether each candidate requirement is good enough to become approved
authority for implementation. This skill does not summarize standards or source
documents; it applies distilled TraceWeaver rules to requirements during
planning and document review.

Core question:

```text
Can this requirement safely become approved authority for implementation?
```

If not, explain why, classify the issue, suggest a rewrite or reclassification
when safe, and state the traceability impact.

## Reference Loading

Load only what the review needs:

- Always load `references/requirements-quality-operating-model.md`,
  `references/requirements-quality-checklist.md`, and
  `references/requirements-review-finding-schema.md` for substantive reviews.
- Load `references/requirement-types-and-attributes.md` when classifying
  requirements or checking metadata.
- Load `references/requirement-language-rules.md` when writing findings about
  ambiguity, weak language, compound requirements, or implementation leakage.
- Load `references/verification-validation-guide.md` when reviewing
  verification methods, ATPs, validation paths, or evidence claims.
- Load `tests/requirements-quality-examples.md` when calibrating examples or
  producing rewrite guidance.
- Load `references/source-basis.md` only when the user asks where the rules came
  from or when updating the distilled knowledge base.

Do not reproduce licensed source text, source tables, source diagrams, or long
quoted passages. Public output must use original TraceWeaver wording.

## Process

### 1. Identify Candidate Requirements

Scan the supplied document, issue, spec, matrix, plan, or acceptance criteria.
For each candidate item, classify it before judging it:

- requirement
- stakeholder need
- goal or idea
- assumption
- design note or implementation decision
- constraint
- acceptance criterion
- verification or validation evidence
- traceability gap

Do not treat every sentence as a requirement. If a sentence is not a
requirement, say what it is and where it should live.

### 2. Classify Type And Authority State

For each real requirement, identify:

- stable ID, or missing ID
- requirement type
- source or parent need
- owner
- status and approval state
- priority and rationale when available
- verification method
- validation path
- version or change history when available

If the requirement lacks enough metadata to act as approved authority, mark it
`Needs revision` or `Blocked`; do not infer approval.

### 3. Run The Quality Gate

Check whether the requirement is:

- necessary
- singular
- unambiguous
- complete enough to interpret
- feasible
- verifiable
- correct against known source context
- consistent with peer requirements
- traceable to a parent need or source
- implementation-neutral unless it is explicitly a constraint
- at the right level of abstraction

Use the score only to summarize quality:

| Score | Meaning | Default Status |
|---:|---|---|
| 5 | Clear, typed, traceable, verifiable, validatable, and approvable | Can approve |
| 4 | Mostly sound with minor metadata or wording edits | Revise |
| 3 | Understandable but incomplete, weakly testable, or missing trace/V&V detail | Revise |
| 2 | Ambiguous, compound, unverifiable, conflicting, or unsafe as authority | Block |
| 1 | Not actually a requirement or mostly a design note/idea | Reclassify |
| 0 | Contradictory, hazardous, or unusable as written | Block |

### 4. Map Verification And Validation

Keep verification and validation separate:

- Verification: did we build it right?
- Validation: did we build the right thing?

For every requirement ask:

- Can this be verified with inspection, analysis, demonstration, or test?
- Is there a measurable pass/fail or review condition?
- Is an ATP, procedure, result expectation, or evidence artifact identified?
- Which need, user scenario, stakeholder review, acceptance path, operational
  dry run, or production signal validates it?
- Is validation missing, deferred, or accepted as an explicit gap?

Do not overclaim ordinary unit tests as validation.

### 5. Decide Approval Readiness

Apply the gate:

| Condition | Reviewer Action |
|---|---|
| Good requirement | Can become approved authority when approval metadata exists |
| Weak requirement | Require revision before approval |
| Ambiguous requirement | Require human decision or clarification |
| Unverifiable requirement | Block or accept only as explicit risk/gap with owner |
| Design note pretending to be requirement | Reclassify as design decision, constraint, or implementation note |
| No parent need/source | Block approval or record traceability gap |

A weak requirement must not become approved authority for implementation.

### 6. Produce The Review Report

Use this report shape unless the user asks for another format:

```markdown
# Requirements Quality Review

## Summary

Reviewed: N requirements
Approved-quality: N
Needs revision: N
Blocked: N
Reclassify: N

## Blocking Issues

| Requirement | Issue | Reason | Action |
|---|---|---|---|

## Requirement Quality Scores

| Requirement | Type | Score | Status |
|---|---|---:|---|

## Findings

[Use the finding schema from references/requirements-review-finding-schema.md]

## Recommendations

1. ...
```

Only suggest a rewrite when the intended behavior is clear. If the source need
or actor is uncertain, ask for human clarification instead of inventing a
requirement.

## Integration With TraceWeaver

Use this skill before `systems-engineering-traceability` treats a requirement
as approved authority. Traceability asks whether behavior is traceable; this
skill asks whether the requirement is good enough to be traced to.

If a requirement fails this review:

- do not mark it `Approved`
- do not let implementation tasks close directly to it as authority
- record the failed checks and traceability impact
- create a revision action, human decision, risk, gap, or reclassification

## Common Rationalizations

| Rationalization | Reality |
|---|---|
| "The intent is obvious." | Future agents need explicit actor, condition, outcome, trace, and V&V path. |
| "We can test it later." | If no verification method is visible, the requirement is not approval-ready. |
| "This is just a planning doc." | Planning docs create implementation authority; weak requirements become weak code. |
| "The design is already chosen." | A design decision is not the same as a requirement unless the constraint is intentional and approved. |
| "The user story covers it." | User stories often mix need, behavior, acceptance, and design; classify the pieces before approval. |
| "A unit test validates it." | A unit test may verify implementation, but validation needs stakeholder or intended-use evidence. |

## Red Flags

- Vague words such as "fast", "easy", "robust", "intuitive", or "user-friendly"
- Escape clauses such as "where possible", "as needed", or "if practical"
- Open-ended lists such as "etc." or "and so on"
- Multiple behaviors joined by "and", "or", "while", or "including" without
  clear decomposition
- Missing actor, condition, measurable outcome, owner, source, or status
- Requirement text that names a database, framework, internal class, or
  algorithm without an approved constraint rationale
- Verification method present but no pass/fail condition
- Validation path missing for user-facing behavior
- Requirement with no parent need, source, or rationale

## Verification

Before finishing the review, confirm:

- [ ] Candidate requirements were separated from ideas, assumptions, design
      notes, constraints, and evidence.
- [ ] Each requirement has a type or a missing-type finding.
- [ ] Each requirement has an approval-readiness decision.
- [ ] Blocked items explain why they cannot become implementation authority.
- [ ] Verification and validation concerns are separate.
- [ ] Suggested rewrites are original and do not copy source material.
- [ ] The report includes traceability impact for every blocking finding.
