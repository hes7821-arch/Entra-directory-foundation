# Entra ID Directory Foundation - Northwind Services

## Project Overview
Northwind Services is a growing 15-person organization transitioning from unmanaged, shared credentials and spreadsheet tracking to a centralized Identity and Access Management (IAM) framework using Microsoft Entra ID. 

This project establishes a standardized directory architecture, role-based access control (RBAC) groups, automated user provisioning pipelines, and audit log auditing to support scalable growth and security compliance.

---

## Business Scenario
Prior to this deployment, Northwind Services lacked standardized user naming, centralized access governance, and structured offboarding boundaries. 

### Organizational Breakdown
| Department | Headcount | Primary Functions & Notes |
| :--- | :--- | :--- |
| **Executive** | 2 | Owner / CEO and Executive support |
| **IT** | 3 | IT Manager, Systems Administrator, Help Desk Support |
| **Finance** | 2 | Payroll and invoicing management |
| **Sales** | 4 | Rapidly growing revenue execution team |
| **HR** | 2 | Onboarding, offboarding, and personnel records |
| **Contractors** | 2 | Non-employee consultants with fixed contract end dates |

---

## Tools Used
* **Identity Platform:** Microsoft Entra ID (Free Tier)
* **Data Structuring:** Microsoft Excel / CSV
* **Documentation & Version Control:** Markdown, Git, GitHub
* **Tenant Domain:** `hes7821gmail515.onmicrosoft.com`

---

## What I Built

### 1. Standardized Naming Conventions
Established UPN and security group conventions to prevent administrative sprawl and facilitate future rule-based access.
* **User Principal Names (UPN):** `firstname.lastname@hes7821gmail515.onmicrosoft.com`
* **Security Group Format:** `SEC-<Type>-<Value>` (e.g., `SEC-Dept-Sales`, `SEC-Role-Helpdesk`, `SEC-Type-Contractor`)

### 2. Identity Provisioning & Bulk Operations
* **Manual Provisioning:** Created the initial 5 administrative and core IT accounts manually to verify full attribute mapping (`displayName`, `userPrincipalName`, `jobTitle`, `department`, `manager`, `usageLocation`).
* **Bulk Import Execution:** Engineered and uploaded `users.csv` to bulk-provision the remaining 10 user accounts while ensuring 100% attribute consistency.

### 3. Role-Based Group Architecture
Created assigned Security groups mapping to business departments and cross-functional roles:
* `SEC-Dept-Executive`
* `SEC-Dept-IT`
* `SEC-Dept-Finance`
* `SEC-Dept-Sales`
* `SEC-Dept-HR`
* `SEC-Role-Helpdesk`
* `SEC-Type-Contractor`

### 4. Group Access Efficiency Analysis (The 16th User)
To measure administrative efficiency, a 16th user (`Chloe Bennett`) was onboarded to the Sales team. We evaluated the administrative overhead required to grant access to 4 core sales applications (Salesforce, Concur, Slack, Outreach):

* **With Group-Based Access:** **2 administrative steps** (Create user + assign to `SEC-Dept-Sales`). Total application grants required across 5 sales reps = **4 grants** (1 grant per app to the group).
* **Without Group-Based Access:** **6 administrative steps** (Create user + 4 individual application assignments). Total application grants required across 5 sales reps = **20 grants** (5 users × 4 apps).

> **Result:** Implementing group-based access reduced access assignment steps by **80%** across the team and eliminated orphaned permission risks during offboarding.

---

## Repository Structure
```text
entra-directory-foundation/
├── README.md
├── users.csv
├── docs/
│   ├── naming-convention.md
│   └── org-design.md
└── screenshots/
    ├── users-list.png
    ├── user-profile-details.png
    ├── groups-list.png
    ├── group-membership.png
    └── audit-log.png