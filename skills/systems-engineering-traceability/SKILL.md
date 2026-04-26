---
name: systems-engineering-traceability
description: Maintains traceability for agent-generated behavior from idea and stakeholder need through requirement, design, implementation, verification, and validation. Use when refining ideas that may become work, starting or changing meaningful behavior, reviewing unclear code, auditing agent output, planning verification, preparing release evidence, or when code lacks a clear requirement, test, validation path, or owner.
---

# Systems Engineering Traceability

## Overview

Maintain the engineering chain that explains why meaningful behavior exists, what requirement it satisfies, where it is implemented, how it is verified, and how it is validated. The goal is to prevent dark code: behavior that runs but cannot be traced to a need, requirement, design decision, evidence, or owner.

This skill is a lifecycle companion to `idea-refine`, `spec-driven-development`, `planning-and-task-breakdown`, `incremental-implementation`, `test-driven-development`, `documentation-and-adrs`, `code-review-and-quality`, and `shipping-and-launch`. It does not replace those skills; it keeps their outputs connected.

## When to Use

Use this skill when:

- Refining, selecting, or summarizing an idea that may become product, project,
  workflow, code, process, or agent behavior
- Starting or changing a feature, module, service, public interface, data flow, automation, or agent workflow
- Modifying behavior that affects users, data, security, operations, integrations, or release readiness
- Reviewing code written by an agent or human where the reason for the behavior is unclear
- Auditing existing code for ownership, requirement coverage, tests, validation, or safe removal
- Preparing verification, validation, release, or acceptance evidence
- A reviewer asks: "Why does this exist?"

Use Lite mode for ordinary small changes with clear intent. Use Standard mode for ambiguous behavior, interfaces, or data-flow changes. Use Audit mode for high-risk, release-critical, compliance-sensitive, or owner-unclear work.

**When NOT to use:** Formatting-only changes, typo-only changes, comment-only changes, or tiny fixes with obvious scope and existing traceability. Even then, be able to state the reason for the change.

## Core Model

Maintain this chain:

```text
Idea/intent -> stakeholder need -> requirement -> design decision -> implementation -> verification -> validation
```

For projects with separate documents, keep this chain connected when those artifacts exist:

```text
requirements.md -> plan.md -> traceability matrix -> ATP -> results
```

ATP means acceptance test plan or acceptance test procedure. Results may be acceptance test results, verification output, or acceptance test report artifacts.

The Markdown traceability matrix is the audit record for trace links, status, evidence references, gaps, and human decisions. Source artifacts remain authoritative for their own detailed content: requirements live in specs, design rationale in ADRs, procedures in ATPs, and measured outcomes in result records. Mermaid diagrams are visual views only.

For the agent-facing lifecycle rules, use `references/systems-engineering-traceability-operating-model.md`.

For a reusable matrix and diagram shape, use `references/traceability-matrix-template.md`.

For requirement quality, ATP/result records, and verification/validation evidence, use `references/requirements-and-vv-guide.md`.

For risk controls, approved gaps, traceability debt, dark-code candidates, and change control, use `references/risk-gap-and-change-control-guide.md`.

## Process

### 1. Select Scope and Mode

Before adding or changing behavior, identify:

- Scope: feature, module, PR, file group, workflow, or release
- Mode: Lite, Standard, or Audit
- Stakeholders: users, operators, maintainers, security, compliance, support, or future agents
- Success signal: what observable result proves this solves the need

Use the lightest mode that preserves the chain. Do not trace every line or every private helper.

### 2. Set Up or Update the Traceability Artifact

When this skill is used, create or update a traceability matrix artifact. For Standard and Audit work, use:

```text
docs/traceability/[scope].md
```

Use the repository's existing traceability location if one already exists.

The artifact should include only the sections needed for the work:

- System context
- Stakeholder needs
- Requirements
- Design decisions or ADR links
- Traceability matrix
- Document chain links
- ATP and result records
- Verification evidence
- Validation evidence or validation plan
- Traceability gaps
- Dark-code candidates
- Human decisions required

Lite mode may use a minimal matrix row in the existing traceability artifact, spec, plan, PR description, or review comment instead of a full matrix. It must not skip the matrix artifact entirely.

### 3. Use Stable IDs

Assign or reuse stable IDs for meaningful items:

```text
NEED-001   Stakeholder need
UREQ-001   User requirement
SREQ-001   System requirement
IF-001     Interface requirement
RISK-001   Risk control
ADR-001    Architecture decision
TASK-001   Implementation task
VER-001    Verification evidence
VAL-001    Validation evidence
TD-001     Traceability debt
GAP-001    Approved traceability gap
DEC-001    Human decision
```

Use feature-scoped IDs when they improve readability, such as `SREQ-AUTH-001` or `VER-BILLING-002`. Do not force long namespaces onto small changes.

### 4. Apply Lifecycle Checkpoints

| Lifecycle phase | Agent question | Required trace update | Block condition |
|---|---|---|---|
| Ideate | What candidate need, assumption, risk, success signal, and failure signal does this idea represent? | Capture idea output as candidate `NEED-*`, assumptions, `RISK-*` candidates, open decisions, and `Candidate` / `Draft` status. | Idea is treated as implementation authority or skips directly into build work. |
| Spec | What stakeholder need and success signal justify this behavior? | Capture or reuse need and requirement IDs; mark inferred items as `Draft`. | Requirement is ambiguous, untestable, contradictory, or unapproved. |
| Plan | Which requirement IDs does each task satisfy? | Link plan/task IDs, acceptance criteria, likely artifacts, verification method, and validation path. | Task has no approved requirement, approved design decision, first-class approved risk control, approved gap, or task-authority closure. |
| Build | Does this implementation still match the traced intent? | Link meaningful files, modules, interfaces, and config to requirement or design IDs; record new gaps immediately. | New meaningful behavior appears without a traced reason. |
| Test | What ATP, test, or evidence proves the requirement? | Link ATP entries, test paths, commands, results, and verification evidence to requirement IDs. | Verification evidence is missing for implemented behavior. |
| Review | Can a reviewer walk backward and forward through the chain? | Review provenance, links, gaps, inferred requirements, and dark-code candidates. | Unapproved inferred links, unexplained behavior, or unresolved dark-code candidates remain. |
| Ship | Is the stakeholder need validated or is a validation path approved? | Link result records, validation evidence, owner, date/session, or approved validation plan. | Stakeholder-facing work lacks validation evidence or an approved validation path. |

### 5. Enforce the No-Orphan-Implementation Gate

Before creating meaningful behavior, identify at least one approved source of system authority:

- Approved requirement ID
- Approved design decision or ADR
- First-class approved risk control
- Approved traceability gap
- Task ID that itself closes directly to one of the above

A Task ID alone is not sufficient traceability. A bare `RISK-*` ID is not sufficient traceability. Implementation tasks are work packages, not sources of system authority. If a task cannot be traced back to an approved requirement, approved design decision, first-class approved risk control, or approved gap, then any implementation produced by that task is still orphaned.

If no source of system authority exists, stop and ask the human whether to create a requirement, approve a gap, or drop the behavior.

Private helpers do not need direct top-level requirement IDs. They inherit traceability through the behavior, module, interface, or risk control they support.

### 6. Use Evidence-Based Status

Traceability status must move only when evidence exists:

| Status | Meaning | Required evidence |
|---|---|---|
| `Draft` | Proposed or inferred; not yet approved. | Source artifact or agent note plus required human decision. |
| `Approved` | Accepted requirement, decision, risk control, or approved gap. | Human approval record with approver, date/session, source artifact, and affected IDs. |
| `Implemented` | Implementation artifacts linked. | Files, modules, interfaces, tasks, or config linked to requirement or design IDs. |
| `Verified` | Technical requirement has evidence. | Test, ATP, build, static analysis, or manual-inspection result linked to the requirement. |
| `Validated` | Stakeholder need satisfied in context. | Demo, UAT, scenario, operational evidence, telemetry, or accepted validation result. |
| `Open` | Item is unresolved and still needs action or decision. | Owner, next action, and affected IDs. |
| `Gap` | Missing, stale, contradictory, or unapproved trace link. | Gap description, risk, owner, and next action. |
| `Deferred` | Valid trace item intentionally postponed. | Owner, reason, expected follow-up, and accepted risk. |
| `Closed` | Traceability debt has been resolved or converted. | Resolution note and linked replacement, approval, or retirement evidence. |
| `Expired` | Approval or accepted gap is no longer valid. | Expiry condition, owner, and required re-approval or closure action. |
| `Retired` | Requirement, behavior, or artifact no longer active. | Deprecation or removal rationale and impact analysis. |

Do not mark agent-inferred requirements as approved, verified, or validated without recorded human approval and evidence.

### 7. Separate Verification From Validation

Verification asks: did we build it right?

Validation asks: did we build the right thing?

Tests usually support verification. Demos, user acceptance, operational scenarios, stakeholder review, staged rollout telemetry, or production feedback usually support validation.

Record verification evidence with the method, command or artifact, result, date/session, requirement ID, and notes. Record validation evidence or an approved validation plan with owner and status when validation must happen after merge.

### 8. Detect Dark Code

Flag any meaningful code, interface, data flow, config, script, test, or automation where you cannot answer:

- Why does this exist?
- Which requirement or risk control does it satisfy?
- Which design decision explains it?
- Where is it implemented?
- How is it verified?
- How is it validated?
- Who owns it?
- What breaks if it is removed?

Classify each candidate:

- Keep and document
- Test and verify
- Validate
- Deprecate
- Remove
- Escalate to human

Dark code does not automatically mean delete it. It means traceability has been lost.

### 9. Perform Scoped Impact Analysis

Run impact analysis when a linked requirement, interface, architecture decision, data flow, risk control, or externally observable behavior changes.

Identify affected:

- Upstream needs
- Downstream requirements
- Design decisions or ADRs
- Components, interfaces, files, and configuration
- Verification evidence that must be updated or rerun
- Validation scenarios that must be rerun or replanned
- Risks, docs, gaps, and human decisions

For ordinary implementation changes that do not affect those triggers, record a trace update or verification note instead of forcing a full impact analysis.

### 10. Apply the Engineering-Complete Gate

Before this skill is complete, every new or changed meaningful behavior must trace to at least one valid approved authority.

Valid approved authority means one of:

- Approved requirement
- Approved ADR or design decision
- First-class approved risk control
- Approved traceability gap
- Task ID that closes directly to one of the approved authorities above

The following are not valid authority by themselves:

- Idea-refinement note
- Brainstorm note
- Roadmap thought
- Bare task ID
- Bare stakeholder need
- Draft requirement
- Inferred requirement
- Unapproved design note
- Bare `RISK-*` ID
- Review finding
- Traceability debt item
- Implementation convenience

If a link is inferred, draft, stale, ambiguous, or not approved, the behavior remains orphaned until human approval resolves it.

Before calling the work complete, also confirm:

- Every meaningful behavior has valid approved authority
- Every changed requirement has linked implementation coverage
- Every implemented behavior has verification evidence or a recorded gap
- Every stakeholder-facing change has validation evidence or an approved validation path
- Requirements docs, plan docs, ATP entries, and result records are linked when they exist
- Dark-code candidates are classified
- Inferred requirements remain `Draft` until approved
- Open gaps and human decisions are visible

## Common Rationalizations

| Rationalization | Reality |
|---|---|
| "The code works, so traceability is unnecessary." | Working code proves execution, not that the right requirement or need was satisfied. |
| "The tests are enough." | Tests usually verify technical behavior; they do not always validate stakeholder fit. |
| "This helper does not need a requirement." | True, but it must inherit traceability through the behavior, module, or interface it supports. |
| "The requirement is obvious." | Obvious requirements become invisible assumptions. Invisible assumptions create dark code. |
| "I'll document it at the end." | End-only traceability often describes what was built, not why it should exist. |
| "The agent inferred the link, so it is fine." | Inferred links are drafts until a human approves them with evidence. |
| "Traceability is too heavy." | Use Lite mode. Trace meaningful behavior, not every line. |

## Red Flags

- Meaningful behavior traces only to a task ID
- Meaningful behavior traces only to a stakeholder need without an approved requirement
- Meaningful behavior traces only to an idea, brainstorm note, or roadmap thought
- A bare `RISK-*` ID is used as authority
- A review finding is treated as authority instead of provenance
- A traceability debt item is treated as authority without being converted into an approved gap
- A requirement or design link is inferred but not approved
- A task does not close directly to approved upstream authority
- A test proves code behavior but not requirement satisfaction
- A stakeholder-facing change has verification evidence but no validation evidence or validation plan
- Requirements, plans, ATP entries, or result records use inconsistent IDs
- The Mermaid diagram disagrees with the matrix
- The agent says "I inferred" without recording a `Draft` item and human decision
- Code exists but nobody can explain what breaks if it is removed

## Verification

Before completing work with this skill, confirm:

- [ ] Scope and mode were selected
- [ ] Ideas that may become work are recorded as candidate needs, assumptions,
      risks, success/failure signals, and open decisions
- [ ] Every new or changed meaningful behavior traces to valid approved authority
- [ ] Stable IDs are assigned or reused
- [ ] The traceability matrix is updated; Lite mode uses at least a minimal matrix row
- [ ] Source artifacts remain authoritative for detailed content
- [ ] Mermaid, if present, matches the matrix IDs
- [ ] Requirements docs, plan docs, ATP entries, and result records are linked when they exist
- [ ] Verification evidence is recorded
- [ ] Validation evidence or an approved validation plan is recorded
- [ ] Dark-code candidates are classified
- [ ] Impact analysis is completed for changed requirements, interfaces, architecture, data flows, risk controls, or externally observable behavior
- [ ] Inferred links remain `Draft` until human approval is recorded
