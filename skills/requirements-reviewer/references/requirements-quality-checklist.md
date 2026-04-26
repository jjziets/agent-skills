# Requirements Quality Checklist

Use this checklist for each candidate requirement. Missing items do not all have
the same severity; judge them by whether the requirement can safely become
approved implementation authority.

## Identity And Authority

- [ ] Has a stable requirement ID.
- [ ] Has a clear requirement type.
- [ ] Has one current text value.
- [ ] Has status: candidate, draft, proposed, approved, rejected, retired, or superseded.
- [ ] Has approval state and approval evidence if marked approved.
- [ ] Has version or change history if it has changed.

## Traceability

- [ ] Traces to a parent need, source, regulation, risk control, or approved decision.
- [ ] Has rationale explaining why it exists.
- [ ] Has owner or accountable role.
- [ ] Has priority, criticality, or ordering signal when tradeoffs are possible.
- [ ] Does not duplicate another requirement.
- [ ] Does not conflict with peer requirements.

## Requirement Text

- [ ] States what must be true.
- [ ] Uses consistent mandatory language.
- [ ] Identifies the system, component, actor, or interface under obligation.
- [ ] Includes conditions, modes, states, or context when they change the obligation.
- [ ] Is singular.
- [ ] Is unambiguous.
- [ ] Is complete enough for implementation and review.
- [ ] Is feasible within known constraints.
- [ ] Is implementation-neutral unless intentionally marked as a constraint.
- [ ] Is at the right abstraction level.

## Measurement And Evidence

- [ ] Is verifiable.
- [ ] Has verification method: inspection, analysis, demonstration, or test.
- [ ] Has measurable pass/fail criteria or review condition.
- [ ] Has ATP/procedure/result expectation when appropriate.
- [ ] Has validation path to stakeholder need, user scenario, operational context, or acceptance signal.
- [ ] Separates verification evidence from validation evidence.

## Blocking Conditions

Block approval when any of these are true:

- [ ] No parent/source/need and no approved rationale.
- [ ] No objective verification path.
- [ ] Actor or obligated system is unclear.
- [ ] Outcome is vague or subjective.
- [ ] Multiple behaviors are combined and cannot be tested independently.
- [ ] It prescribes design without approved constraint rationale.
- [ ] It conflicts with another approved requirement.
- [ ] It is actually a task, idea, design note, or assumption.

## Review Outcome

Choose exactly one:

- `Can approve`: quality, traceability, V&V, and approval metadata are sufficient.
- `Revise`: useful requirement but wording, metadata, trace, or V&V needs work.
- `Block`: unsafe as authority due to ambiguity, unverifiability, conflict, or missing source.
- `Human decision`: intent cannot be safely inferred.
- `Reclassify`: useful text but not a requirement.
