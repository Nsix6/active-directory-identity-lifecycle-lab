# National Digital Identity Authority (NDIA)

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

NDIA
│
├── Executives
├── HumanResources
├── Finance
├── Legal
├── Audit
├── IdentityOperations
├── Technology
├── Security
├── CitizenServices
├── RegionalOffices
│
├── ServiceAccounts
├── PrivilegedAccounts
├── Servers
├── Workstations
├── Groups
├── Contractors
└── DisabledUsers

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

- Standard Engineering user accounts belong in the existing `Technology` OU.

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
