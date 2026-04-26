# Requirements Quality Examples

These are original TraceWeaver examples. Do not copy examples from licensed
sources into runtime material.

## Example: Vague Requirement

Bad:

```text
The system should be fast and easy to use.
```

Finding:

- vague language
- not verifiable
- no workload, threshold, or user scenario
- weak mandatory language

Better:

```text
The search service shall return the first page of results within 2 seconds for
95% of searches under normal operating load.
```

Verification:

- Performance test using representative query mix and normal operating load.

Validation:

- User acceptance scenario for the search workflow confirms the response time is
  acceptable for the intended task.

## Example: Escape Clause

Bad:

```text
The system shall send alerts as needed when problems occur.
```

Finding:

- escape clause
- trigger unclear
- recipient unclear
- no evidence condition

Better:

```text
The monitoring service shall send an incident alert to the on-call channel
within 60 seconds when a production health check fails for 3 consecutive probes.
```

Verification:

- Test or demonstration that injects failed probes and records alert timing.

Validation:

- Operations dry run confirms the alert reaches the right responder in the
  expected workflow.

## Example: Compound Requirement

Bad:

```text
The user shall upload documents and receive a warning when unsupported file
types are selected.
```

Finding:

- compound requirement
- upload behavior and warning behavior need separate verification

Better:

```text
SREQ-DOC-001: The upload service shall accept PDF documents up to 20 MB.
SREQ-DOC-002: The upload interface shall display an unsupported-file warning
before upload when the selected file type is not in the approved file type list.
```

Verification:

- Upload test for accepted PDF size.
- UI or integration test for unsupported-file warning.

Validation:

- User scenario confirms unsupported documents are caught before the user waits
  for a failed upload.

## Example: Implementation Leakage

Bad:

```text
The system shall use Redis to store checkout sessions.
```

Finding:

- implementation-biased unless Redis is an approved constraint
- does not state required behavior

Better if Redis is not an approved constraint:

```text
The checkout service shall preserve an active checkout session for 30 minutes
after the user's last checkout action.
```

Better if Redis is an approved constraint:

```text
CON-CHK-001: The checkout service shall store active checkout session state in
the approved Redis cluster to satisfy the platform session-state constraint.
```

Verification:

- Session persistence test after inactivity.
- Constraint inspection if Redis is approved authority.

Validation:

- Checkout continuation scenario confirms users can resume the intended flow.

## Example: Missing Parent Need

Bad:

```text
SREQ-014: The system shall export audit data every night.
```

Finding:

- may be clear and verifiable
- parent need/source is missing
- rationale and owner are missing

Better:

```text
SREQ-AUD-014: The audit service shall export the previous day's audit events to
the compliance archive by 02:00 UTC each day.
```

Required metadata:

- Parent: NEED-COMP-002 or regulatory/source reference.
- Owner: compliance platform owner.
- Rationale: compliance archive must receive daily evidence.

Verification:

- Scheduled job test or production result record showing export completion.

Validation:

- Compliance reviewer confirms the archive supports the required audit workflow.

## Example: Validation Missing

Bad:

```text
The onboarding flow shall collect all required company profile fields.
```

Finding:

- could be verifiable
- validation path missing
- "required fields" needs source or closed field list

Better:

```text
The onboarding flow shall require the company profile fields listed in
PROFILE-FIELDS-001 before the account can be submitted for review.
```

Verification:

- Form validation test for each field in `PROFILE-FIELDS-001`.

Validation:

- Onboarding stakeholder review confirms the submitted profile supports the
  account review workflow.

## Example: Not A Requirement

Bad:

```text
Create a new React hook for loading the billing plan.
```

Finding:

- task or design note
- not a requirement
- no user or system outcome

Better as requirement:

```text
The billing settings page shall display the account's current billing plan
before the user can change plan options.
```

Better as task:

```text
TASK-BILL-004: Implement the billing-plan loading mechanism for SREQ-BILL-002.
```

Traceability impact:

- The task must close to an approved requirement or design decision before it
  can authorize implementation.
