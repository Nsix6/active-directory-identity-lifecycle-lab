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
| Active Directory | ⏳ |
| Entra ID | ⏳ |
| RBAC | ⏳ |
| Identity Lifecycle | Checklist reviewed; AD implementation and execution testing pending |
 
## Structure
 
The layout below includes planned module folders. Day 3 documentation and evidence are saved under `identity_lifecycle_day_3/`.

```text
active-directory-identity-lifecycle-lab
├── foundations
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
