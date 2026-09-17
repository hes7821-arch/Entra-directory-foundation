# Microsoft Entra ID: Least Privilege & Admin Roles Lab

## Project Overview
This project demonstrates the design, deployment, and testing of a least-privilege Role-Based Access Control (RBAC) architecture for a 16-person organization in Microsoft Entra ID. The environment enforces strict administrative boundaries, establishes emergency break-glass procedures, and audits administrative role assignments.

## Business Scenario
Northwind Services required delegated administrative roles for helpdesk operations, user management, and IT oversight without over-provisioning tenant-wide permissions. The identity strategy enforces the Principle of Least Privilege (PoLP) to minimize the attack surface and limit potential lateral movement or privilege escalation in the event of account compromise.

## Tools Used
* **Identity Platform:** Microsoft Entra ID (Free Tier)
* **Authentication:** Microsoft Authenticator (MFA)
* **Source Control:** Git & GitHub

## What I Built
* **Delegated Role Matrix:** Assigned scoped roles to key personnel (**Helpdesk Administrator** to David Chen, **User Administrator** to Alex Mercer, and **Reports Reader** to Marcus Vance).
* **Non-Privileged Baseline:** Maintained zero administrative roles for 12 standard organizational accounts.
* **Access Boundary Validation:** Tested and verified explicit permission blocks by signing in as a scoped administrator and attempting unauthorized actions.
* **Emergency Access Strategy:** Deployed an emergency Global Administrator account with documented policy exclusion frameworks.
* **Audit Trail Verification:** Validated directory audit logs tracking administrative role changes.

## Documentation Deliverables
* [`docs/lab2/ticket-exercise.md`](docs/lab2/ticket-exercise.md) — Rationale for all 6 help desk ticket scenarios.
* [`docs/lab2/role-assignment-rationale.md`](docs/lab2/role-assignment-rationale.md) — Comprehensive role assignment justifications, metrics, and governance analysis.
* [`docs/lab2/break-glass.md`](docs/lab2/break-glass.md) — Emergency access account setup and policy exclusion strategy.

## Key Screenshots
* [`screenshots/lab2/action-blocked-boundary.png`](screenshots/lab2/action-blocked-boundary.png) — Password reset panel verifying David Chen's boundary testing on user accounts.
* [`screenshots/lab2/audit-log-role-assignment.png`](screenshots/lab2/audit-log-role-assignment.png) — Directory Audit Logs tracking role modification events (`Add member to role`).
* [`screenshots/lab2/role-assignment 1-confirmation.png`](screenshots/lab2/role-assignment%201-confirmation.png) — User Administrator role confirmation for Alex Mercer.
* [`screenshots/lab2/roles-assignment 2-confirmation.png`](screenshots/lab2/roles-assignment%202-confirmation.png) — Helpdesk Administrator role confirmation for David Chen.
* [`screenshots/lab2/roles-assignment 3-confirmation.png`](screenshots/lab2/roles-assignment%203-confirmation.png) — Reports Reader role confirmation for Marcus Vance.
* [`screenshots/lab2/roles-privileged-label 1.png`](screenshots/lab2/roles-privileged-label%201.png) — Entra All Roles directory view highlighting built-in `PRIVILEGED` labels.
* [`screenshots/lab2/roles-privileged-label 2.png`](screenshots/lab2/roles-privileged-label%202.png) — Entra All Roles view showing User Administrator and Global Administrator privileged classifications.

## Security Lessons Learned
* **Least Privilege Limits Blast Radius:** Least privilege is not about distrusting employees; it is about limiting how far a single compromised account can go. An assistant with a narrow password-reset role getting phished is an isolated incident. A Global Administrator getting phished is a full tenant takeover, extending across attached cloud infrastructure.
* **Permissions Depend on the Target:** "Resetting a password" is not a monolithic permission—it splits into distinct privilege levels depending on the target account. Resetting a standard user requires *Helpdesk Administrator*, resetting a limited admin requires *User Administrator*, and resetting a Global Admin requires *Privileged Authentication Administrator*. Any permission that allows changing authentication factors represents a direct privilege escalation vector.

## Future Improvements
* **Role-Assignable Groups:** Shift from direct user assignments to group-based role assignments (requires Entra ID P1).
* **Just-In-Time (JIT) Access:** Implement Privileged Identity Management (PIM) so administrative rights are activated on-demand rather than held permanently (requires Entra ID P2).
* **Administrative Units:** Scope regional or department administrators using Administrative Units (requires Entra ID P1).
* **Access Governance:** Conduct automated, periodic access reviews on administrative role holders (requires Entra ID Governance).
* **Phishing-Resistant MFA:** Implement FIDO2 hardware security keys for emergency break-glass accounts.
* **Automated Security Alerting:** Configure real-time alerts via Log Analytics/Sentinel whenever an emergency access account initiates a session.
