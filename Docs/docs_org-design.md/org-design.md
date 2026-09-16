# Identity & Access Management Design Document

## 1. Group Architecture & Business Justification
To implement Role-Based Access Control (RBAC) and adhere to the Principle of Least Privilege, Northwind Services uses 7 Security Groups under a standardized `sec-<type>-<value>` naming convention:

* **`sec-dept-executive`**: Grants top-tier corporate access, board reporting apps, and high-level financial dashboards.
* **`sec-dept-it`**: Assigns baseline administrative tooling, infrastructure access, and internal ticketing portals.
* **`sec-dept-finance`**: Controls access to accounting platforms, payroll software, and general ledgers.
* **`sec-dept-sales`**: Authorizes CRM access, lead distribution tools, and expense reporting applications.
* **`sec-dept-hr`**: Restricts access to sensitive employee records, PII, and HRIS systems.
* **`sec-role-helpdesk`**: Provides Tier-1 support technicians elevated permissions for password resets and service desk queues without granting full IT tenant admin rights.
* **`sec-type-contractor`**: Acts as an isolation and tracking group to apply stricter, time-bound Conditional Access policies and restricted resource access.

---

## 2. Departmental Grouping Strategy & Scalability Limits
Grouping by department creates a clean, intuitive baseline because organizational structures rarely change overnight. 

* **Where it strains:** Department-only grouping breaks down when cross-functional projects occur, when employees hold dual responsibilities, or when matrixed reporting requires application-level access that spans multiple departments (e.g., an HR Manager needing access to Finance tools for benefits administration).

---

## 3. Contractor Identity Management
Contractors are isolated using a dedicated category group (`sec-type-contractor`) rather than being granting blanket department membership. 

* **Design Decision:** Contractors do not inherit permanent staff entitlements. By segmenting contractors into `sec-type-contractor`, we ensure that security policies—such as mandatory 30-day credential rotation, restricted guest permissions, and strict session timeouts—apply universally regardless of the work they perform.

---

## 4. Enterprise Scaling Considerations (500 Users vs. 15 Users)
At 15 users, static assigned membership is simple to manage manually. At 500+ users, static assignment leads to role explosion, configuration drift, and stale access permissions. At scale:

1. **Dynamic Membership:** Upgrade to Microsoft Entra ID P1/P2 to replace manual assignment with rules based on user attributes (e.g., `user.department -eq "Sales"` automatically populates `sec-dept-sales`).
2. **Access Reviews:** Establish quarterly automated access reviews requiring managers to re-certify employee permissions.
3. **Log Archiving:** Export tenant audit logs to Azure Log Analytics or Microsoft Sentinel, bypassing the 7-day Free tier retention limit for long-term compliance storage.

---

## 5. Iterative Refinement & Design Corrections
During the initial buildout, group naming syntax varied between uppercase (`SEC-`) and lowercase (`sec-`). While Entra ID evaluation is case-insensitive, inconsistent syntax creates friction in automated PowerShell/API pipelines and degrades audit readability. All groups were standardized to lowercase `sec-` prefixes to maintain a single naming convention across the environment.