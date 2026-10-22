# Active Directory Identity Lifecycle Lab
 
A hands-on identity and access management lab covering:
 
- Identity Foundations
- Active Directory
- Microsoft Entra ID
- RBAC
- Identity Lifecycle Management
- Group Policy
- Privileged Access Management
 
## Daily progress

| Day | Topic | Status |
| --- | --- | --- |
| [01](labs/day-01-identity-foundations/README.md) | Identity foundations | IAM glossary and NDIA organization documented |
| [02](labs/day-02-protocol-foundations/README.md) | Protocol foundations | No saved artifacts; documentation pending |
| [03](labs/day-03-identity-lifecycle/README.md) | Identity lifecycle | Checklist and document review complete; AD execution pending |
| [04](labs/day-04-directory-basics/README.md) | Directory basics | Domain/OU design and document review complete; AD deployment pending |

## Modules
 
| Module | Status |
|----------|----------|
| Foundations | ✅ |
| Active Directory | Day 4 domain/OU design reviewed; deployment and live testing pending |
| Entra ID | ⏳ |
| RBAC | ⏳ |
| Identity Lifecycle | Checklist reviewed; AD implementation and execution testing pending |
 
## Structure
 
Daily work lives under `labs/day-NN-topic/`, using two-digit day numbers and lowercase names separated by hyphens. Each day has a README describing its objective, artifacts, and status.

```text
active-directory-identity-lifecycle-lab/
├── README.md
└── labs/
    ├── day-01-identity-foundations/
    │   ├── README.md
    │   └── docs/
    ├── day-02-protocol-foundations/
    │   └── README.md
    ├── day-03-identity-lifecycle/
    │   ├── README.md
    │   ├── docs/
    │   └── evidence/
    └── day-04-directory-basics/
        ├── README.md
        ├── architecture/
        │   └── ad-domain-design.md
        └── evidence/
            └── day-04-verification.md
```

Within each day, use `docs/` for notes and checklists, `architecture/` for designs and diagrams, `scripts/` for automation, `tests/` for repeatable validation, and `evidence/` for actual results and sanitized outputs. Create subfolders when they contain work; the Day 1 image files are retained in their existing relative locations within that day's folder.

Keep one authoritative copy of each design or script in the day where it was introduced. Later days link to and update that copy as needed, while Git records changes and each day's evidence records what was verified. The Day 4 domain design is the current directory design for NDIA.

## Day 3 — Identity lifecycle

**Milestone:** Create the lifecycle checklist for the AD project.

**Status:** Lifecycle checklist created and document review passed; AD implementation and execution testing pending.

- [John's joiner, mover, and leaver scenario](labs/day-03-identity-lifecycle/docs/doc.md)
- [AD identity lifecycle checklist](labs/day-03-identity-lifecycle/docs/lifecycle-checklist.md)
- [Checklist review and evidence](labs/day-03-identity-lifecycle/evidence/checklist-review.md)

The checklist defines an owner, trigger, access change, verification step, and rollback step for each lifecycle event. The document review confirmed all 15 required fields are populated and consistent with the scenario; live AD behavior remains untested.

## Day 4 — Directory basics

**Milestone:** Design the `adlab.test` domain and its OU structure for NDIA.

**Status:** One-forest, one-domain design completed and reviewed against all seven Day 4 checks; deployment and live AD testing pending.

- [NDIA domain, OU, group, and access design](labs/day-04-directory-basics/architecture/ad-domain-design.md)
- [Day 4 verification, expected versus actual results, and deviations](labs/day-04-directory-basics/evidence/day-04-verification.md)
- [Assigned reading: Introduction to AD DS](https://learn.microsoft.com/en-us/training/modules/introduction-to-ad-ds/)

The design includes the five required OUs, places employee accounts within NDIA departments, defines proposed security groups and test-share permissions, and maps John's joiner, mover, and leaver controls to directory objects. The foundations diagram and Day 3 checklist reference the refined hierarchy; this repository update does not claim that AD is deployed or that the reading assessment has been completed.
