# Requirement Types And Attributes

Classify each candidate before reviewing quality. Type affects abstraction,
evidence, owner, and validation path.

## Requirement Type Taxonomy

| Type | Meaning | Example Use | Review Focus |
|---|---|---|---|
| Stakeholder Need | Problem, outcome, or capability expected by a stakeholder | Early discovery and validation target | Is the need clear enough to derive requirements? |
| User Requirement | User-visible capability, behavior, or constraint | Product/user language | Does it connect user outcome to acceptance? |
| System Requirement | Required system behavior, property, or constraint | Engineering authority | Is it implementable, verifiable, and traceable? |
| Software Requirement | Required behavior or quality allocated to software | Software planning and test | Is allocation clear and not over-prescriptive? |
| Interface Requirement | Required interaction between systems, components, people, or organizations | APIs, protocols, handoffs, data exchange | Are boundary, direction, data, timing, and error behavior clear? |
| Functional Requirement | Required function or behavior | "The system shall..." behavior | Is the behavior singular and condition-bound? |
| Quality Requirement | Non-functional property such as usability, reliability, maintainability, observability, scalability, or accessibility | Quality attributes | Is there measurable evidence? |
| Performance Requirement | Timing, throughput, latency, capacity, or resource use | Service levels and load behavior | Are workload, percentile, context, and threshold defined? |
| Security Requirement | Protection, access, audit, privacy, or abuse-resistance obligation | Auth, data handling, threat controls | Is threat/source and verification evidence clear? |
| Safety Requirement | Hazard avoidance, mitigation, or fail-safe behavior | Safety-critical operation | Is hazard, condition, and acceptance evidence explicit? |
| Operational Requirement | Behavior needed in deployment, support, recovery, monitoring, or maintenance | Runbooks, support, uptime | Is operational context and owner known? |
| Constraint | A mandatory limit on design, technology, process, regulation, or environment | "Must use approved identity provider" | Is the constraint intentional, sourced, and approved? |
| Validation Criterion | Condition used to decide whether a need is satisfied in context | User acceptance, scenario success | Is it tied to need, stakeholder, and acceptance signal? |

## Minimum Useful Attributes

| Attribute | Required For Approval? | Purpose |
|---|---:|---|
| `id` | Yes | Stable trace key |
| `type` | Yes | Review lens and evidence expectations |
| `text` | Yes | The actual obligation |
| `source_or_parent_need` | Yes | Why the requirement exists |
| `owner` | Yes | Accountable human or role |
| `status` | Yes | Lifecycle state |
| `approval_state` | Yes | Whether it may be used as authority |
| `priority` | Usually | Tradeoff and sequencing |
| `criticality` | When relevant | Safety, security, compliance, or delivery risk |
| `rationale` | Yes | Decision context and intent |
| `verification_method` | Yes | How satisfaction is proven |
| `verification_criteria` | Yes | Pass/fail or review condition |
| `validation_path` | Yes | How user/stakeholder need is validated |
| `version` | Yes after change | Change control |
| `change_history` | Yes after change | Auditability |
| `assumptions` | When relevant | Conditions that may invalidate the requirement |
| `risks_or_gaps` | When relevant | Known weakness or accepted uncertainty |

## Status Values

Use consistent status language:

| Status | Meaning | Authority? |
|---|---|---:|
| Candidate | Captured from idea, need, source, or review | No |
| Draft | Being shaped, incomplete, or agent-inferred | No |
| Proposed | Ready for human review | No |
| Approved | Accepted as implementation authority | Yes |
| Implemented | Implementation exists | Depends on approval |
| Verified | Evidence shows requirement satisfied | Depends on evidence |
| Validated | Evidence shows need satisfied in context | Depends on evidence |
| Rejected | Not accepted | No |
| Superseded | Replaced by another item | No |
| Retired | No longer active | No |

Do not mark a requirement approved, verified, or validated by inference.

## Type-Specific Pitfalls

- User requirements that hide multiple system requirements.
- System requirements written as UI tasks or database design.
- Quality requirements without measurable thresholds.
- Performance requirements without workload or percentile.
- Interface requirements without direction, data contract, failure behavior, or ownership.
- Security requirements without asset, actor, threat, or control.
- Constraints with no source or rationale.
- Validation criteria mistaken for verification tests.
