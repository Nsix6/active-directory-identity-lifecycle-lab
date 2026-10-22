# Active Directory Identity Lifecycle Lab
 
A hands-on identity and access management lab covering:
 
- Identity Foundations
- Active Directory
- Microsoft Entra ID
- RBAC
- Identity Lifecycle Management
- Group Policy
- Privileged Access Management
 
## Modules
 
| Module | Status |
|----------|----------|
| Foundations | ✅ |
| Active Directory | Day 4 domain/OU design reviewed; deployment and live testing pending |
| Entra ID | ⏳ |
| RBAC | ⏳ |
| Identity Lifecycle | Checklist reviewed; AD implementation and execution testing pending |
 
## Structure
 
The layout below includes planned module folders. Day 3 artifacts are under `identity_lifecycle_day_3/`; Day 4 design and verification are under `architecture/` and `evidence/`.

```text
active-directory-identity-lifecycle-lab
├── foundations
├── architecture
│   └── ad-domain-design.md
├── evidence
│   └── day-04-verification.md
├── active-directory
├── entra-id
├── rbac
├── identity-lifecycle
└── identity_lifecycle_day_3
    ├── docs
    └── evidence
```

## Day 3 — Identity lifecycle

**Milestone:** Create the lifecycle checklist for the AD project.

**Status:** Lifecycle checklist created and document review passed; AD implementation and execution testing pending.

- [John's joiner, mover, and leaver scenario](identity_lifecycle_day_3/docs/doc.md)
- [AD identity lifecycle checklist](identity_lifecycle_day_3/docs/lifecycle-checklist.md)
- [Checklist review and evidence](identity_lifecycle_day_3/evidence/checklist-review.md)

The checklist defines an owner, trigger, access change, verification step, and rollback step for each lifecycle event. The document review confirmed all 15 required fields are populated and consistent with the scenario; live AD behavior remains untested.

## Day 4 — Directory basics

**Milestone:** Design the `adlab.test` domain and its OU structure for NDIA.

**Status:** One-forest, one-domain design completed and reviewed against all seven Day 4 checks; deployment and live AD testing pending.

- [NDIA domain, OU, group, and access design](architecture/ad-domain-design.md)
- [Day 4 verification, expected versus actual results, and deviations](evidence/day-04-verification.md)
- [Assigned reading: Introduction to AD DS](https://learn.microsoft.com/en-us/training/modules/introduction-to-ad-ds/)

The design includes the five required OUs, places employee accounts within NDIA departments, defines proposed security groups and test-share permissions, and maps John's joiner, mover, and leaver controls to directory objects. The foundations diagram and Day 3 checklist reference the refined hierarchy; this repository update does not claim that AD is deployed or that the reading assessment has been completed.
