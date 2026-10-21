# Day 3 — Lifecycle Checklist Review

**Review date:** 21 October 2026 (Africa/Lagos)

**Milestone:** Create the lifecycle checklist for the AD project.

**Artifact reviewed:** [AD identity lifecycle checklist](../docs/lifecycle-checklist.md)

**Supporting documents:** [John's lifecycle scenario](../docs/doc.md) and [NDIA organization and OU design](../../foundations/README.md).

## Test scope and method

This was a document review of the planned AD lifecycle controls. A read-only structural check confirmed the required fields were present and non-empty, followed by a manual review of their meaning and consistency with John's scenario and the NDIA design.

No AD accounts, groups, permissions, sessions, or OUs were changed or tested. Microsoft Entra ID Governance automation was not configured or tested. The execution checkboxes remain unchecked because the AD implementation has not been run.

## Expected outcome

Joiner, Mover, and Leaver must each contain an owner, trigger, access change, verification step, and rollback step: 15 populated fields in total. The controls must follow the same test identity through Engineering onboarding, transfer to Security Operations with approved Engineering read-only access, and departure with account disablement and resource-access removal.

## Actual result

All 15 required fields are present and non-empty. Manual review found that the entries describe the same proposed account, `john.test`, and use the existing planned `Technology`, `Security`, and `DisabledUsers` OUs consistently.

| Event | Owner | Trigger | Access change | Verification | Rollback | Manual review finding |
| --- | --- | --- | --- | --- | --- | --- |
| Joiner | Present | Present | Present | Present | Present | Defines HR confirmation, manager approval, a standard Engineering account, approved file access, permitted and denied access checks, and reversal of failed onboarding. |
| Mover | Present | Present | Present | Present | Present | Reuses John's account, removes Engineering write access, requires approval for retained read access, adds proposed Security monitoring access, and checks for unintended remaining permissions. Restoration of old access requires approval. |
| Leaver | Present | Present | Present | Present | Present | Defines authorized departure timing, account disablement, resource-access removal, session checks, placement in `DisabledUsers`, and controlled restoration if the departure is cancelled. |

### Sanitized structural check output

The read-only check inspected each lifecycle section for its five required, populated table rows. This output demonstrates document structure only; the manual findings above assess the written controls.

```text
Joiner: PASS (5/5 required fields present and non-empty)
Mover: PASS (5/5 required fields present and non-empty)
Leaver: PASS (5/5 required fields present and non-empty)
Total: PASS (15/15 required fields present and non-empty)
```

## Differences and remaining implementation work

No missing required fields or contradictions with John's written lifecycle scenario were found in the checklist. The checklist expands the scenario with proposed test account, group, role, and resource names; these are design definitions, not evidence of existing AD configuration.

Actual sign-in, file access, group membership changes, session termination, OU policy effects, and rollback behavior remain untested. Their expected-versus-actual execution results must be recorded when the AD lab is built; this review does not establish that those controls work in a running environment.

## How this supports Identity Foundations and AD Lab Setup

This checklist turns the NDIA identity lifecycle scenario into defined responsibilities, triggers, access changes, verification criteria, and recovery actions for the AD build. It provides the requirements for implementing and testing John's account, OU placement, and group-based resource access across joining, transferring, and leaving.

**Review result:** PASS for checklist completeness and documented scenario consistency; AD execution testing remains pending.
