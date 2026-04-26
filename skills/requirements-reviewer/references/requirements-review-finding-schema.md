# Requirements Review Finding Schema

Use structured findings when a requirement cannot safely become approved
authority or needs revision. Prefer one finding per distinct issue.

## Finding Record

```yaml
finding_id: REQ-FIND-001
requirement_id: SREQ-001
requirement_text: "..."
requirement_type: system_requirement
quality_score: 2
severity: block
failed_checks:
  - ambiguous
  - not_verifiable
issue: "The requirement uses subjective quality language without a measurable pass/fail condition."
recommended_action: rewrite
suggested_rewrite: "..."
verification_concern: "No objective verification method or pass/fail condition is defined."
validation_concern: "No user scenario, stakeholder review, or acceptance signal is linked."
traceability_impact: "Should not become approved implementation authority until revised."
human_approval_required: true
```

## Required Fields

| Field | Purpose |
|---|---|
| `finding_id` | Stable finding key |
| `requirement_id` | Requirement affected, or `unassigned` if missing |
| `requirement_text` | Exact reviewed text when safe to include |
| `requirement_type` | Current or recommended type |
| `quality_score` | 0-5 summary score |
| `severity` | `block`, `major`, `minor`, or `note` |
| `failed_checks` | Machine-readable issue tags |
| `issue` | Plain explanation |
| `recommended_action` | `rewrite`, `split`, `reclassify`, `add_metadata`, `add_vv`, `resolve_conflict`, `human_decision`, or `accept_gap` |
| `verification_concern` | Verification issue or `none` |
| `validation_concern` | Validation issue or `none` |
| `traceability_impact` | Why this matters for implementation authority |
| `human_approval_required` | `true` when authority or scope cannot be inferred safely |

## Severity

| Severity | Meaning |
|---|---|
| `block` | Requirement must not become approved authority as written |
| `major` | Requirement is useful but needs revision before approval |
| `minor` | Requirement can likely be approved after small edit or metadata fix |
| `note` | Observation, classification advice, or downstream improvement |

## Failed Check Tags

Use consistent tags:

- `missing_id`
- `missing_type`
- `missing_parent_or_source`
- `missing_owner`
- `missing_approval_state`
- `ambiguous`
- `vague_language`
- `escape_clause`
- `open_ended_list`
- `compound`
- `not_singular`
- `incomplete`
- `not_feasible`
- `not_verifiable`
- `missing_verification_method`
- `missing_validation_path`
- `implementation_biased`
- `wrong_abstraction_level`
- `duplicate`
- `conflict`
- `not_requirement`
- `design_note`
- `assumption`
- `task_not_authority`

## Report Tables

Use these tables before detailed findings:

```markdown
## Blocking Issues

| Requirement | Issue | Reason | Action |
|---|---|---|---|
| SREQ-004 | Not verifiable | Uses subjective language without measurable criteria | Rewrite |

## Requirement Quality Scores

| Requirement | Type | Score | Status |
|---|---|---:|---|
| SREQ-001 | functional_requirement | 5/5 | Can approve |
| SREQ-004 | quality_requirement | 2/5 | Revise |
| SREQ-007 | design_note | 1/5 | Reclassify |
```

## Suggested Rewrite Rule

Suggested rewrites must be original and must not copy source text. Provide a
rewrite only when the requirement intent is clear. Otherwise, set:

```yaml
suggested_rewrite: null
recommended_action: human_decision
```
