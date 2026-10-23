# Day 4 — Directory Basics Verification

**Original review date:** 21 October 2026 (Africa/Lagos)

**Updated scope review:** 23 October 2026 (Africa/Lagos)

**Organization:** National Digital Identity Authority (NDIA), fictional.

**Artifact:** [AD domain and OU design](../architecture/ad-domain-design.md)

**Result:** PASS for the written design requirements. No AD objects were created or tested.

## Scope and method

Review the design against the seven Day 4 checks. Compare the organization with the [Day 1 NDIA description](../../day-01-identity-foundations/README.md) and John's account changes with the [Day 3 lifecycle checklist](../../day-03-identity-lifecycle/docs/lifecycle-checklist.md).

The 23 October review simplifies the documents to directory basics. It removes detailed configuration instructions and advanced naming details, while retaining the folder-access example required by the study plan. The original review date is retained to distinguish the first review from this revision.

## Expected outcome and actual result

| Check | Expected result | Actual result from the updated document review | Outcome |
| --- | --- | --- | --- |
| 1. Forest and domain | Define one forest and one domain and explain the choice. | One forest contains the single `adlab.test` domain. The design explains that NDIA's departments can be organized within it using OUs and groups. | PASS |
| 2. Required OUs | Include Users, Groups, Workstations, Servers, and ServiceAccounts. | All five appear beneath the NDIA OU. | PASS |
| 3. Object locations | Give users, computers, and groups appropriate locations. | Standard users belong in department OUs, group objects in Groups, and workstation/server computer accounts in their respective OUs. The future DC is identified separately in Domain Controllers. | PASS |
| 4. Group purposes | Define every proposed security group's purpose. | Six groups have stated members and purposes: GG_Engineering, GG_Audit, GG_Helpdesk, Engineering_Project_RW, Engineering_Project_Read, and Security_Monitoring_Read. | PASS |
| 5. Folder-access example | Map at least one group to a protected folder or administrative responsibility. | The Engineering Project Folder is mapped to its planned write-access and read-only groups. Audit membership alone grants no Engineering access. Configuration details are left for later work. | PASS |
| 6. Lifecycle support | Explain joiner, mover, and leaver behavior. | John starts in Technology, moves to Security with changed group memberships, and is later disabled and moved to DisabledUsers. | PASS |
| 7. Evidence | Record expected results, actual results, and differences. | This record documents the review results, NDIA adaptations, file checks, and the scope of the exercise. | PASS |

- [x] One forest and one domain are defined.
- [x] All five required OUs appear in the design.
- [x] Users, computers, and groups have appropriate locations.
- [x] Every proposed security group has a defined purpose.
- [x] At least one group is mapped to a protected folder or administrative responsibility.
- [x] The design explains how joiner, mover, and leaver events will work.
- [x] Expected results, actual results, and differences are recorded.

These checks concern the written design. They do not claim that the proposed access works in a running AD environment.

## Differences from the study plan's example

- The required OUs are beneath an NDIA parent OU to match the fictional organization.
- Engineering and Helpdesk users belong in Technology, while Audit users have their own department OU. The suggested group names are retained.
- Existing NDIA departments, PrivilegedAccounts, and DisabledUsers are retained for continuity with Days 1 and 3; each has a simple object-placement explanation.
- Three access-group names from Day 3 are retained so John's scenario remains consistent. Extra administration and configuration details introduced in the first Day 4 draft have been removed.

No required Day 4 design element was found missing in the updated review.

## File checks

Run from the repository root:

```sh
test -f labs/day-04-directory-basics/architecture/ad-domain-design.md && echo "Design file: PASS"
test -f labs/day-04-directory-basics/evidence/day-04-verification.md && echo "Verification file: PASS"
```

Expected: both files exist and both commands print PASS. Actual results from the 23 October check:

```text
Design file: PASS
Verification file: PASS
```

These commands verify file presence. The review table above assesses the written design.

## How this supports the AD lab

The design explains where NDIA's users, computers, and groups should belong in the planned directory. It connects those locations to John's joiner, mover, and leaver scenario so the later AD build has a clear starting point.
