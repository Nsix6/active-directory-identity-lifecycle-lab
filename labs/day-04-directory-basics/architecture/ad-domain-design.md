# Day 4 — NDIA AD Domain and OU Design

**Design date:** 21 October 2026 (Africa/Lagos)

**Organization:** National Digital Identity Authority (NDIA), a fictional government agency

**Status:** Design complete; deployment and live access tests pending.

This document is the implementation design for the directory described in the [NDIA foundations](../../day-01-identity-foundations/README.md) and [John's Day 3 lifecycle checklist](../../day-03-identity-lifecycle/docs/lifecycle-checklist.md). All accounts, groups, servers, shares, and delegations below are proposed test objects. No domain controller is deployed by this exercise.

## Directory concepts in this lab

| Concept | Meaning and NDIA example |
| --- | --- |
| Forest | The AD DS structure sharing schema and configuration across its domains, and the security boundary for the directory. NDIA uses one forest with root domain `adlab.test`. |
| Domain | A directory partition providing domain identities, authentication, and replication scope. `adlab.test` is the only domain; departments do not need separate domains. |
| Domain controller (DC) | A server running AD DS that holds directory data and authenticates domain identities. Proposed `NDIA-DC01` will serve this domain when the lab is built. |
| Organizational unit (OU) | An administrative container for objects, delegation, and Group Policy scope. `Technology` holds standard Engineering and Helpdesk staff accounts. |
| User | An account representing an identity. `john.test` is the fictional employee account; a service identity has a separate purpose and placement. |
| Security group | A collection of security principals used for permissions or delegated rights. `Engineering_Project_RW` will receive Engineering share permissions. Membership and configured permissions grant access; OU placement alone does not. |

These relationships follow Microsoft's [AD logical model](https://learn.microsoft.com/en-us/windows-server/identity/ad-ds/plan/understanding-the-active-directory-logical-model). A domain or OU within the forest is not an independent forest security boundary.

## Forest, domain, and DC decisions

| Setting | Decision | Reason |
| --- | --- | --- |
| Forest count | 1 | NDIA is one fictional organization administered by one lab team; there is no requirement for independently isolated directory administration. |
| Forest root domain | `adlab.test` | Uses the namespace required by the study plan for this local test lab. |
| Domain count | 1 | OUs and groups can represent the departments and access requirements without introducing child domains or trusts. |
| Domain DNS name | `adlab.test` | One directory namespace keeps account placement and lifecycle changes easy to inspect. |
| Domain distinguished name | `DC=adlab,DC=test` | Base for the planned object paths below. |
| NetBIOS domain name | `ADLAB` | Proposed short domain name; for example, `ADLAB\john.test`. |
| Initial DC | `NDIA-DC01.adlab.test` | Planned AD DS and DNS server for the later local VM build; a single DC is sufficient for this introductory lab but provides no DC redundancy. |

The DC computer account remains in the domain's default `Domain Controllers` OU. `Servers` below is for member servers, such as the proposed file server `NDIA-FS01`, rather than domain controllers. OS installation, IP addressing, DNS configuration, redundancy, and Entra integration are later build work.

## OU hierarchy

`[OU]` marks an OU, not a security group or a file share. The `NDIA` OU contains lab-managed objects; the default `Domain Controllers` OU remains outside it.

```text
Forest: adlab.test
Domain: adlab.test (DC=adlab,DC=test)
├── [OU] Domain Controllers                 (default; future NDIA-DC01)
└── [OU] NDIA
    ├── [OU] Users
    │   ├── [OU] Executives
    │   ├── [OU] HumanResources
    │   ├── [OU] Finance
    │   ├── [OU] Legal
    │   ├── [OU] Audit
    │   ├── [OU] IdentityOperations
    │   ├── [OU] Technology                 (Engineering and Helpdesk teams)
    │   ├── [OU] Security
    │   ├── [OU] CitizenServices
    │   ├── [OU] RegionalOffices
    │   └── [OU] Contractors
    ├── [OU] Groups
    ├── [OU] Workstations
    ├── [OU] Servers
    ├── [OU] ServiceAccounts
    ├── [OU] PrivilegedAccounts
    └── [OU] DisabledUsers
```

Create `OU=Users,OU=NDIA,DC=adlab,DC=test` as a custom OU. It is distinct from the built-in `CN=Users,DC=adlab,DC=test` container; do not treat those paths as interchangeable or put lab users in that default container by accident.

### OU purposes and object placement

Paths in this table are relative to `adlab.test`. IT administrators own directory configuration; business managers approve resource access.

| OU path | Purpose | Objects that belong here |
| --- | --- | --- |
| `NDIA` | Parent for NDIA-managed lab objects and explicitly scoped baseline policies. | Child OUs; no ordinary users or computers placed directly here. |
| `NDIA/Users` | Scope standard employee administration and user policies. | Department and contractor OUs. |
| `NDIA/Users/Executives` | Represent the Director General's office. | Standard executive and office staff user accounts. |
| `NDIA/Users/HumanResources` | Represent HR identity-request staff. | Standard HR user accounts. |
| `NDIA/Users/Finance` | Represent Finance & Procurement. | Standard Finance & Procurement user accounts. |
| `NDIA/Users/Legal` | Represent Legal & Compliance. | Standard Legal & Compliance user accounts. |
| `NDIA/Users/Audit` | Scope Internal Audit staff administration. | Standard auditor accounts, for example `auditor.test`. |
| `NDIA/Users/IdentityOperations` | Represent identity operations personnel. | Standard Identity Operations user accounts. |
| `NDIA/Users/Technology` | Scope Technology Services staff administration. | Standard Engineering and Helpdesk staff accounts, including `john.test` before transfer. |
| `NDIA/Users/Security` | Scope Security Operations staff administration. | Standard Security Operations accounts, including `john.test` after transfer. |
| `NDIA/Users/CitizenServices` | Represent Citizen Services personnel. | Standard Citizen Services user accounts. |
| `NDIA/Users/RegionalOffices` | Represent regional staff within the same domain. | Standard regional staff accounts; no extra regional domain is required. |
| `NDIA/Users/Contractors` | Separate contractor account administration and future expiry controls. | Standard contractor user accounts with approved sponsors. |
| `NDIA/Groups` | Organize the proposed custom security groups. | All groups in the group catalog below; not user or computer accounts. |
| `NDIA/Workstations` | Scope workstation administration and computer policies. | Member workstation computer accounts, for example `NDIA-WS01`. |
| `NDIA/Servers` | Scope member-server administration and computer policies. | Member server computer accounts, for example `NDIA-FS01`; excludes DCs. |
| `NDIA/ServiceAccounts` | Separate non-human identities and their ownership records. | Dedicated test service identities, for example `svc.labreport`; no employee accounts. |
| `NDIA/PrivilegedAccounts` | Separate administrative identities from ordinary daily-use identities. | Dedicated admin accounts, for example `helpdesk.admin.test`; the OU itself grants no privileges. |
| `NDIA/DisabledUsers` | Retain disabled departed-user accounts for review. | Disabled employee or contractor accounts after offboarding. Account disablement is a separate action from moving the object. |

The department OUs preserve NDIA's original names. Engineering and Helpdesk are teams within Technology Services, recorded through role/title attributes and groups rather than additional team OUs. This is an intentional adaptation of the study plan's example: all five required OUs exist, while the hierarchy remains consistent with NDIA and Day 3. Microsoft's [OU design guidance](https://learn.microsoft.com/en-us/windows-server/identity/ad-ds/plan/reviewing-ou-design-concepts) supports choosing OU boundaries for policy and delegation rather than copying every business team.

### Administration and Group Policy scope

Technology Services IT administrators create objects and manage OU structure, group membership, and policies. HR supplies approved personnel changes; departmental managers approve resource access without receiving broad directory administration rights.

`GG_Helpdesk` is planned to receive only password-reset and account-unlock delegation on standard user accounts in `Technology`, `Audit`, and `Security`. Its designated administrative accounts belong in `PrivilegedAccounts`. It receives no rights over that OU, `ServiceAccounts`, `DisabledUsers`, group membership, or domain administration. Delegation is a later explicit ACL configuration, not an automatic consequence of the group name.

Plan user baselines on `NDIA/Users`, workstation baselines on `NDIA/Workstations`, and member-server baselines on `NDIA/Servers`. Review inherited settings before applying parent policies and after transfers between department OUs. Privileged and service accounts need separately reviewed policies; no GPOs are created or claimed to be enforced here.

## Security group catalog and protected resources

Every group below is a proposed **Global security group** in `OU=Groups,OU=NDIA,DC=adlab,DC=test`. This small, single-domain exercise uses explicit account membership in resource groups and assigns those groups permissions directly; group nesting is not assumed. Role groups identify teams, while separately approved resource groups control John's file access. Microsoft's [security group documentation](https://learn.microsoft.com/en-us/windows-server/identity/ad-ds/manage/understand-security-groups) describes security group permissions and Global scope.

| Group | Planned members and purpose | Permission or responsibility | Approver |
| --- | --- | --- | --- |
| `GG_Engineering` | Standard Engineering accounts; role membership for onboarding and transfers. | Team classification; no file permissions merely from this membership. | Technology Services Manager |
| `GG_Audit` | Standard Internal Audit accounts. | Read the test Audit Reports share; no automatic Engineering or Security share access. | Internal Audit Manager |
| `GG_Helpdesk` | Dedicated, approved Helpdesk admin accounts. | The limited password-reset/unlock delegation described above; no default domain-admin or resource-share access. | Technology Services Manager |
| `GG_SecurityOperations` | Standard Security Operations accounts. | Team classification; monitoring access requires separate resource-group approval. | Security Operations Manager |
| `Engineering_Project_RW` | Approved Engineering workers, including John on joining. | Read, create, and edit Engineering Project Share files; no permission-management rights. | Technology Services Manager |
| `Engineering_Project_Read` | Explicitly approved readers, including John after transfer. | Read Engineering Project Share files; no create/edit rights. | Technology Services Manager |
| `Security_Monitoring_Read` | Approved Security monitoring staff, including John after transfer. | Read the test Security Monitoring Logs share; no log modification or permission-management rights. | Security Operations Manager |

| Protected resource | Proposed location | Granted access | Required negative check |
| --- | --- | --- | --- |
| Engineering Project Share | `\\NDIA-FS01\EngineeringProjects` | `Engineering_Project_RW`: read/create/edit; `Engineering_Project_Read`: read. | John's Mover state cannot create or edit files. `GG_Audit` alone grants no access. |
| Security Monitoring Logs | `\\NDIA-FS01\SecurityMonitoringLogs` | `Security_Monitoring_Read`: read. | John cannot read it as an Engineering Joiner or modify its logs as a Mover. |
| Audit Reports | `\\NDIA-FS01\AuditReports` | `GG_Audit`: read. | John receives no access from either his Engineering or Security role. |

These UNC paths are proposed test shares, not folders inside AD OUs. During the later build, configure and verify both share and NTFS permissions, including inherited or direct grants that could broaden access. Ordinary resource groups must not receive permission-management rights. Resource-owner and file-server administrative access must be separately controlled; none of the employee roles implies that access.

## Joiner, mover, and leaver mapping

The event owners, triggers, verification, and rollback controls remain defined in the [Day 3 checklist](../../day-03-identity-lifecycle/docs/lifecycle-checklist.md). This table supplies concrete directory paths and adds role-group membership changes to that plan.

| Event | Account and placement | Required group/access change | Planned verification |
| --- | --- | --- | --- |
| Joiner | Create `john.test` in `OU=Technology,OU=Users,OU=NDIA,DC=adlab,DC=test`; approved activation date; Technology Services / Software Engineer attributes. | Add `GG_Engineering` and `Engineering_Project_RW`; no Security, Audit, or privileged memberships. | Confirm account attributes and path, allowed Engineering read/create/edit, denied permission changes, and denied Security/Audit resources. |
| Mover | Keep the same account; update department/title/manager and move to `OU=Security,OU=Users,OU=NDIA,DC=adlab,DC=test`. | Remove `GG_Engineering` and `Engineering_Project_RW`; add `GG_SecurityOperations`, `Security_Monitoring_Read`, and separately approved `Engineering_Project_Read`. Remove any other obsolete grants. | Use a fresh sign-in to confirm Engineering read-only and Security log read access, deny write access to both, and inspect residual permissions and OU policy effects. |
| Leaver | Disable `john.test`, then move to `OU=DisabledUsers,OU=NDIA,DC=adlab,DC=test`; retain the record for review. | Remove role and resource memberships, including `GG_SecurityOperations`, `Engineering_Project_Read`, and `Security_Monitoring_Read`; remove direct resource grants and close applicable resource sessions. | Confirm disabled status and placement, denied new domain authentication, and denied access to all test shares, including previously active sessions. |

An OU move does not itself update team memberships, remove resource access, or disable the account. Follow the approved event and rollback controls rather than relying on the folder-like appearance of the tree.

## Validation and later build boundary

The [Day 4 verification record](../evidence/day-04-verification.md) checks the seven study-plan requirements against this design. File existence and link checks supplement manual design review; they do not demonstrate working AD permissions or authentication.

The design provides object-placement and access requirements for a future test-only VM build. Domain creation, OU/group creation, delegation, GPO application, share ACLs, sign-in tests, session handling, and rollback tests remain pending. Reading and Microsoft Learn assessment completion are not certified by this repository update.

## Study reference

Use Microsoft's [Introduction to AD DS module](https://learn.microsoft.com/en-us/training/modules/introduction-to-ad-ds/) from Introduction through Summary, including the assessment. The module covers the directory concepts used here; the subsequent domain-controller/FSMO module is outside this Day 4 assignment.
