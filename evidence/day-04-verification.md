# Day 4 — Directory Basics Verification

**Review date:** 21 October 2026 (Africa/Lagos)

**Organization:** National Digital Identity Authority (NDIA), fictional

**Artifact:** [AD domain and OU design](../architecture/ad-domain-design.md)

**Result:** PASS for design review; deployment and live testing pending.

## Scope and method

Review the saved design against the seven Day 4 study-plan checks. Compare object placement and group/access definitions with the [NDIA foundations](../foundations/README.md) and [John's lifecycle controls](../identity_lifecycle_day_3/docs/lifecycle-checklist.md), and check repository file presence and local links.

This is design evidence. No Windows Server was installed and no domain, DC, OU, user, group, GPO, delegation, or share was created in AD during this work. No live authentication, permission, session-removal, or rollback tests were run. Microsoft Learn reading and assessment completion are not inferred from these artifacts.

## Expected outcome and actual result

| Check | Expected result | Actual result from document review | Outcome |
| --- | --- | --- | --- |
| 1. Forest and domain | Define one forest and one domain and explain the choice. | The design defines forest root and sole domain `adlab.test`, base `DC=adlab,DC=test`, and explains why one organization/lab team does not require extra domains or trusts. | PASS |
| 2. Required OUs | Include `Users`, `Groups`, `Workstations`, `Servers`, and `ServiceAccounts`. | All five are children of `NDIA`; employee department OUs are under `Users`. The hierarchy also retains NDIA's `PrivilegedAccounts` and `DisabledUsers`. | PASS |
| 3. Object locations | Place users, computers, and groups appropriately. | Standard users go to department OUs, groups to `Groups`, workstations/member servers to their respective OUs, and service/admin identities to separate OUs. The future DC remains in the default `Domain Controllers` OU. | PASS |
| 4. Group purposes | Define every proposed group's members and responsibility. | Seven Global security groups have explicit purposes and approvers: `GG_Engineering`, `GG_Audit`, `GG_Helpdesk`, `GG_SecurityOperations`, `Engineering_Project_RW`, `Engineering_Project_Read`, and `Security_Monitoring_Read`. | PASS |
| 5. Resource or delegation mapping | Map at least one group to a protected folder or administrative responsibility. | Three proposed shares have group-to-permission mappings and negative tests. `GG_Helpdesk` has a narrowly scoped password-reset/unlock delegation proposal rather than broad administrator rights. | PASS |
| 6. Lifecycle support | Explain joiner, mover, and leaver behavior for the same identity. | `john.test` moves from `Technology` to `Security`, loses Engineering write access, retains only approved read access, and is eventually disabled, stripped of resource access, and moved to `DisabledUsers`. Team-group changes, session checks, and Day 3 rollback references are included. | PASS |
| 7. Evidence | Record expected results, actual results, and differences. | This file records the seven review outcomes, command evidence, deviations from the example, and the distinction between reviewed design and unexecuted AD tests. | PASS |

- [x] One forest and one domain are defined.
- [x] All five required OUs appear in the design.
- [x] Users, computers, and groups have appropriate locations.
- [x] Every proposed security group has a defined purpose.
- [x] At least one group is mapped to a protected folder or administrative responsibility.
- [x] The design explains how joiner, mover, and leaver events will work.
- [x] Expected results, actual results, and differences are recorded.

The checked boxes above certify document review, not deployed AD behavior. The Day 3 execution checkboxes remain uncompleted.

## Differences and design decisions

1. **NDIA parent and department OUs:** The plan's five required OUs are placed beneath an `NDIA` parent. Existing department names are preserved beneath `Users` instead of retaining the original flat foundations sketch.
2. **Engineering and Helpdesk placement:** The example's separate team OUs are represented by standard accounts in `Technology`, role/title attributes, and `GG_Engineering` / `GG_Helpdesk`. Audit retains its own departmental OU. This meets the mandatory OU requirements while matching NDIA's Technology Services department and the Day 3 scenario.
3. **Lifecycle continuity:** `Security`, `PrivilegedAccounts`, and `DisabledUsers` extend the five-OU minimum to support NDIA's documented transfer, administration, and departure controls. The domain design supplies full paths; the foundations and Day 3 documents link to it.
4. **Permission-group names:** The three Day 3 resource-group names are retained. The study plan's `GG_Engineering`, `GG_Audit`, and `GG_Helpdesk` are also defined; group objects are not mislabeled as OUs. Direct account membership in resource groups is deliberate for this introductory single-domain lab.

No mandatory Day 4 design requirement was found missing. Live permission outcomes and delegation behavior have no actual execution result yet; they remain future build tests rather than successful results in this record.

## Sanitized command evidence

Run from the repository root:

```sh
test -f architecture/ad-domain-design.md && echo "Design file: PASS"
test -f evidence/day-04-verification.md && echo "Verification file: PASS"
```

Expected: both files exist and both commands print PASS. A separate read-only check also resolved every local Markdown link and checked code-fence pairs in the five created or updated documents.

Actual output:

```text
Design file: PASS
Verification file: PASS
Local document links: PASS (14 checked)
Markdown code fences: PASS (5 documents checked)
```

File-presence checks do not establish technical AD correctness. The manual review matrix above provides the design assessment; local-link checks confirm that supporting artifacts are reachable within the repository.

## How this supports the AD lab

The design converts NDIA's organization and identity lifecycle controls into planned domain, OU, account, group, and resource locations for the upcoming AD build. The verification record supplies acceptance criteria for later provisioning, permission checks, and rollback tests without claiming those tests have already run.
