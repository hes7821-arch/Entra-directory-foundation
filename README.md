# Microsoft Entra ID: Directory & Group Foundation (Lab 1)

## Project Overview
This project demonstrates the initial provision and architecture of a 16-user enterprise directory in Microsoft Entra ID. The deployment establishes organizational departments, assigns standardized security groups, and enforces identity governance standards.

## Business Scenario
Northwind Services required a structured cloud directory setup to support scaled onboarding, department-level access controls, and administrative boundary management.

## Tools Used
* **Identity Platform:** Microsoft Entra ID (Free Tier)
* **Bulk Provisioning:** PowerShell / CSV Upload
* **Source Control:** Git & GitHub

## What I Built
* **User Provisioning:** Populated 16 organizational users across Finance, Sales, HR, IT, Executive, and Contractor departments.
* **Security Group Structure:** Created 7 Security Groups utilizing the standardized `Sec-` naming convention.
* **Access Mapping:** Assigned all 16 users to their respective department security groups.

## Naming Conventions
All groups follow the `Sec-` title-case standard:
* `Sec-Dept-Executive`
* `Sec-Dept-Finance`
* `Sec-Dept-IT`
* `Sec-Dept-Sales`
* `Sec-Dept-HR`
* `Sec-Dept-Contractors`

## Documentation Deliverables
* [Organizational Design Document](Docs/docs_org_design.md)
* [Naming Conventions Standard](docs/naming-convention.md)

## Key Screenshots
* [All Users Verification](Screenshots/all-users.png)
* [All Groups Verification](Screenshots/all-groups.png)
* [Group Membership Detail](Screenshots/group-membership.png)

## Security Lessons Learned
* **Group-Based Access Governance:** Assigning permissions directly to individual users leads to privilege creep and tracking failures. Managing access strictly through security groups ensures scalable onboarding and offboarding.
* **Audit Log Retention Constraints:** Entra ID Free retains audit logs for only 7 days. Production environments require shipping logs to Azure Monitor / Microsoft Sentinel for compliance and long-term investigation.
* **Credential Hygiene in Version Control:** Bulk import templates (`users.csv`) must have plain-text passwords stripped or redacted prior to committing to public repositories.

## Future Improvements
* **Dynamic Group Membership:** Configure automated membership rules using attributes (e.g., `user.department -eq "Sales"`) with Entra ID P1 licensing.
* **Access Reviews:** Establish automated access reviews for sensitive security groups.
* **SIEM Integration:** Stream directory logs directly to a Microsoft Sentinel workspace.
