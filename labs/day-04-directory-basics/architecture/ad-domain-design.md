# Day 4 — NDIA AD Domain and OU Design

**Design date:** 21 October 2026 (Africa/Lagos)

**Scope reviewed:** 23 October 2026 (Africa/Lagos)

**Organization:** National Digital Identity Authority (NDIA), a fictional government agency.

**Status:** Written design complete. No directory objects have been created in AD for this exercise.

## Day 4 objective

Understand forests, domains, domain controllers, organizational units (OUs), users, and security groups. Design the `adlab.test` domain, explain where objects belong, and connect the structure to John's joiner, mover, and leaver scenario.

The organization comes from the [Day 1 NDIA description](../../day-01-identity-foundations/README.md). John's scenario comes from the [Day 3 lifecycle checklist](../../day-03-identity-lifecycle/docs/lifecycle-checklist.md).

## Directory concepts

AD DS means **Active Directory Domain Services**, the directory service used to store and manage the lab's accounts, computers, and groups.

| Concept | Meaning | NDIA example |
| --- | --- | --- |
| Forest | A collection of one or more AD domains. | NDIA's forest contains only `adlab.test`. |
| Domain | A named part of the directory containing accounts, computers, and groups managed together. | `adlab.test` is NDIA's only planned domain. |
| Domain controller (DC) | A server running AD DS that stores directory information and checks users' sign-in details. | `NDIA-DC01` is the proposed name of the future DC. |
| Organizational unit (OU) | A container used to organize directory objects. It also supports Group Policy (rules for users and computers) and delegation (assigning specific administration tasks). | The `Technology` OU contains standard Engineering and Helpdesk user accounts. |
| User | An account representing a person or a service. | `john.test` represents John, the fictional employee. |
| Security group | A collection of accounts used to assign access or responsibilities together. | `Engineering_Project_RW` groups people who should receive Engineering project-folder access. |

A user account belongs in an OU and can be a member of security groups. The OU organizes the account; the security groups are used when assigning access. A folder containing project files is a separate resource, not an OU.

## One forest and one domain

| Decision | Reason |
| --- | --- |
| One forest, identified by its first domain `adlab.test` | NDIA is one fictional organization managed by one lab team. This exercise does not require additional forests. |
| One domain named `adlab.test` | The study plan requires this name. NDIA's departments can be organized using OUs and groups within this domain. |
| One proposed domain controller named `NDIA-DC01` | Gives the future directory server a name in the design. Installing that server is later work. |

## OU structure

Every entry marked `[OU]` is an organizational unit. These are proposed locations, not objects already created in AD.

```text
Forest: adlab.test
Domain: adlab.test
├── [OU] Domain Controllers             (default location for the future DC)
└── [OU] NDIA
    ├── [OU] Users
    │   ├── [OU] Executives
    │   ├── [OU] HumanResources
    │   ├── [OU] Finance
    │   ├── [OU] Legal
    │   ├── [OU] Audit
    │   ├── [OU] IdentityOperations
    │   ├── [OU] Technology             (Engineering and Helpdesk teams)
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

`NDIA/Users` is a planned OU for this lab, separate from the default Users container supplied by AD. The slash-separated locations below describe the diagram; they are not commands.

### OU purposes and object locations

| OU location | Purpose and objects |
| --- | --- |
| `NDIA` | Parent OU for the organization's lab objects, organized into the child OUs below. |
| `NDIA/Users` | Parent OU for standard employee and contractor accounts, organized by department. |
| `NDIA/Users/Executives` | Standard user accounts for the Director General's office. |
| `NDIA/Users/HumanResources` | Standard HR user accounts. |
| `NDIA/Users/Finance` | Standard Finance & Procurement user accounts. |
| `NDIA/Users/Legal` | Standard Legal & Compliance user accounts. |
| `NDIA/Users/Audit` | Standard Internal Audit user accounts. |
| `NDIA/Users/IdentityOperations` | Standard Identity Operations user accounts. |
| `NDIA/Users/Technology` | Standard Engineering and Helpdesk user accounts, including John before his transfer. |
| `NDIA/Users/Security` | Standard Security Operations user accounts, including John after his transfer. |
| `NDIA/Users/CitizenServices` | Standard Citizen Services user accounts. |
| `NDIA/Users/RegionalOffices` | Standard regional-office user accounts. |
| `NDIA/Users/Contractors` | Standard contractor user accounts. |
| `NDIA/Groups` | The proposed security group objects listed below. |
| `NDIA/Workstations` | Workstation computer accounts, such as the proposed `NDIA-WS01`. |
| `NDIA/Servers` | Computer accounts for servers other than domain controllers. |
| `NDIA/ServiceAccounts` | Accounts used by software or services rather than employees. |
| `NDIA/PrivilegedAccounts` | Separate accounts used for administrative tasks, as already proposed in the NDIA foundations. |
| `NDIA/DisabledUsers` | Disabled accounts retained after employees leave, matching the Day 3 scenario. |
| `Domain Controllers` | The default OU for domain controller computer accounts, including the future `NDIA-DC01`. |

This includes all five required OUs: **Users, Groups, Workstations, Servers, and ServiceAccounts**. Engineering and Helpdesk remain teams within NDIA's Technology Services department; Audit has its own department OU. This adapts the study plan's example to the existing fictional organization.

## Proposed security groups

All groups below are planned objects in `NDIA/Groups`. The `GG_` prefix follows the study plan's example naming convention; these entries are groups, not OUs. The other three group names are retained from Day 3 so the two exercises use the same names.

| Group | Planned members | Purpose |
| --- | --- | --- |
| `GG_Engineering` | Engineering user accounts. | Identify NDIA's Engineering team. Folder access is assigned separately through the relevant access group below. |
| `GG_Audit` | Internal Audit user accounts. | Assign read access to a proposed Audit Reports folder. |
| `GG_Helpdesk` | Helpdesk user accounts within Technology Services. | Group Helpdesk staff for their role; the name alone gives no administrative rights. |
| `Engineering_Project_RW` | Engineering users approved for project work, including John on joining. | Assign read, create, and edit access to the Engineering Project Folder. |
| `Engineering_Project_Read` | Approved readers, including John after transfer. | Assign read-only access to the Engineering Project Folder. |
| `Security_Monitoring_Read` | Approved Security Operations users, including John after transfer. | Assign read access to the proposed Security Monitoring Logs folder. |

### Required folder-access example

The Engineering Project Folder is the same resource called the Engineering Project Share in Day 3. At the design level, `Engineering_Project_RW` is intended to receive read, create, and edit access, while `Engineering_Project_Read` is intended to receive read-only access. Membership in `GG_Audit` alone should not give a user access to Engineering project files.

This satisfies the requirement to connect at least one security group to a protected folder. Creating the folders and applying their permissions are later lab work.

## How the structure supports John's lifecycle

| Event | Account and OU change | Group and access change |
| --- | --- | --- |
| Joiner | John joins as a Software Engineer. His proposed account `john.test` belongs in `NDIA/Users/Technology`. | Add him to `GG_Engineering` and the approved `Engineering_Project_RW` group for Engineering project work. |
| Mover | John transfers to Security Operations. Keep his account, update his role and department, and move it to `NDIA/Users/Security`. | Remove Engineering team membership and Engineering write access. Assign approved `Engineering_Project_Read` and `Security_Monitoring_Read` membership for his new responsibilities. |
| Leaver | John leaves NDIA. Disable his account and move it to `NDIA/DisabledUsers`. | Remove his remaining work-related group memberships and access. |

Moving an account between OUs does not itself change its group memberships or disable it. The [Day 3 checklist](../../day-03-identity-lifecycle/docs/lifecycle-checklist.md) contains the separate lifecycle controls; Day 4 explains where the objects belong.

## Day 4 validation

The [verification record](../evidence/day-04-verification.md) checks the written design against all seven Day 4 requirements. This exercise produces documents, not a running directory.

## Assigned reference

Read Microsoft's [Introduction to AD DS](https://learn.microsoft.com/en-us/training/modules/introduction-to-ad-ds/) from Introduction through Summary, including the module assessment. This design covers the six directory concepts and the domain/OU design required by the Day 4 plan.
