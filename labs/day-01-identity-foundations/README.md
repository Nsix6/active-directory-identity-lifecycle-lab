# Day 1 — Identity Foundations

**Focus:** Establish IAM vocabulary and define the fictional organization used by later labs.

**Status:** The IAM glossary and NDIA organization are documented. The directory structure below is a planned design.

- [Identity glossary](docs/identity-glossary.md)
- [Current NDIA domain design from Day 4](../day-04-directory-basics/architecture/ad-domain-design.md)
- [Daily progress index](../../README.md)

## National Digital Identity Authority (NDIA)

## Overview

The National Digital Identity Authority (NDIA) is a fictional government agency responsible for managing national digital identities, citizen authentication services, biometric enrollment, identity verification, and secure access to government digital services.

This organization is designed for use in an Active Directory, Microsoft Entra ID, Identity and Access Management (IAM), and Identity Lifecycle Management lab environment.

---

# Organizational Structure

NDIA
│
├── Office of the Director General
│
├── Human Resources
├── Finance & Procurement
├── Legal & Compliance
├── Internal Audit
├── Identity Operations
├── Technology Services
├── Security Operations
├── Citizen Services
└── Regional Offices

---

# Active Directory Organizational Unit (OU) Structure

The [Day 4 domain design](../day-04-directory-basics/architecture/ad-domain-design.md) defines the planned `adlab.test` directory. It refines the original department-based sketch by placing standard department accounts under a custom `Users` OU and separating groups, computers, service identities, and administrative identities.

```text
adlab.test
├── Domain Controllers                 (default OU; future NDIA-DC01)
└── NDIA
    ├── Users
    │   ├── Executives
    │   ├── HumanResources
    │   ├── Finance
    │   ├── Legal
    │   ├── Audit
    │   ├── IdentityOperations
    │   ├── Technology                 (Engineering and Helpdesk)
    │   ├── Security
    │   ├── CitizenServices
    │   ├── RegionalOffices
    │   └── Contractors
    ├── Groups
    ├── Workstations
    ├── Servers
    ├── ServiceAccounts
    ├── PrivilegedAccounts
    └── DisabledUsers
```

All entries below the domain in this diagram are OUs. The proposed `GG_*` security groups are separate objects stored in `NDIA/Groups`; no objects have been deployed yet.

---

# Department Structure

## Office of the Director General

### Roles

- Director General
- Executive Assistant
- Chief of Staff

### Resources

- Executive Portal
- Strategic Planning Repository
- Board Reports

---

## Technology Services

### Team

- Engineering

### Roles

- Software Engineer
- Technology Services Manager

### Active Directory Placement

- Standard Engineering user accounts are planned for `OU=Technology,OU=Users,OU=NDIA,DC=adlab,DC=test`, as defined in the Day 4 design.

### Resources

- Engineering Project Share: a test file share for Engineering project files and documentation.

### Required Access

- Software Engineers can read, create, and edit files in the Engineering Project Share through an Engineering security group.
- This access does not include managing share permissions or granting access to others.
- Membership in the `Technology` OU alone does not grant access to the share.

### Access Approver

- The Technology Services Manager approves access to the Engineering Project Share.
- An IT administrator implements and verifies the approved security group membership changes.

---
