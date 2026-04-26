# Requirement Language Rules

Requirement language must make authority clear. The goal is not ceremonial
wording; the goal is one interpretation, one obligation, and a visible evidence
path.

## Preferred Structure

Use this structure when formal requirement language is appropriate:

```text
The [system/component/interface] shall [required behavior or property]
[under condition/context] [with measurable outcome].
```

If the project does not use strict `shall` language, use consistent mandatory
language such as `must` or `is required to`. Avoid mixing mandatory and optional
language in the same requirement set.

## Required Language Qualities

| Quality | Rule |
|---|---|
| Mandatory | Use binding language for approved requirements. |
| Singular | One obligation per requirement. |
| Active | Name the system, actor, or component under obligation. |
| Conditional when needed | State modes, states, triggers, workloads, environments, or preconditions that affect behavior. |
| Measurable | Include threshold, range, outcome, state, artifact, or review condition when quality depends on evidence. |
| Implementation-neutral | State what must be true, not the internal design, unless it is a sourced constraint. |

## Weak Or Vague Words

Flag subjective terms unless the requirement defines measurable criteria:

| Weak Word | Why It Fails | Better Direction |
|---|---|---|
| fast | no threshold or workload | response time, throughput, percentile, load |
| easy | subjective | task completion rate, steps, user acceptance scenario |
| robust | broad and unverifiable | availability, recovery, error handling, tolerance |
| scalable | no dimension | max users, events, data volume, latency under load |
| secure | too broad | specific control, asset, threat, audit, access rule |
| reliable | broad | uptime, error budget, recovery time, failure rate |
| intuitive | subjective | usability scenario or measured outcome |
| appropriate | hides decision | define condition and acceptance criterion |
| sufficient | hides threshold | state minimum acceptable value or evidence |

## Escape Clauses

Flag escape clauses unless they are intentionally governed:

- where possible
- as needed
- if practical
- as appropriate
- normally
- generally
- should
- may
- optionally

If optional behavior is intentional, it should be a design option, policy, or
conditional requirement with a decision rule.

## Open-Ended Lists

Flag:

- etc.
- and so on
- including but not limited to
- such as
- for example

Use a closed list for authority. If the list is illustrative, it is probably
guidance, not a requirement.

## Compound Requirement Patterns

Split requirements that combine independent obligations:

- two or more behaviors joined by `and`
- alternatives joined by `or` without a decision rule
- behavior plus implementation approach
- user-visible outcome plus internal design
- normal behavior plus error behavior
- performance plus security plus usability in one sentence

Compound requirements create ambiguous verification because one part may pass
while another fails.

## Implementation Leakage

Flag requirement text that prescribes how to build when the design is not an
approved constraint:

- database, table, queue, or framework selection
- internal class, package, or algorithm names
- UI component choice where user outcome is what matters
- deployment topology where service quality is the need
- test implementation details inside requirement text

Reclassify implementation leakage as:

- `constraint` if sourced and approved
- `ADR` or design decision if it explains a chosen design
- implementation task if it is work to do
- rewritten requirement if the design is unnecessary

## Rewrite Examples

These examples are original and intentionally generic.

| Problem | Weak Text | Better Requirement Direction |
|---|---|---|
| Vague performance | "The dashboard should load fast." | "The dashboard shall render the initial summary view within 2 seconds for 95% of requests under normal operating load." |
| Escape clause | "The service should retry failed syncs where possible." | "The service shall retry failed sync attempts up to 3 times within 10 minutes when the upstream returns a transient error." |
| Compound | "The user shall upload files and receive alerts when processing fails." | Split upload behavior and failure alert behavior into separate requirements. |
| Implementation leakage | "The system shall store users in PostgreSQL." | If storage choice is not a constraint: "The system shall persist user account records so they remain available after service restart." |
| Missing condition | "The system shall lock accounts." | "The system shall lock an account for 15 minutes after 5 failed login attempts within 10 minutes." |
| Unverifiable quality | "The UI shall be user-friendly." | "A first-time user shall complete the setup workflow in 5 minutes or less using the published setup instructions." |

## Safe Rewrite Rule

Only propose a concrete rewrite when the intended actor, outcome, condition, and
source need are clear. If any of those are uncertain, recommend clarification
instead of inventing scope.
