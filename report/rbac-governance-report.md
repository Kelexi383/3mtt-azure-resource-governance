# Role-Based Access Control (RBAC) Governance Report

## 1. Security Design Principle
To enforce a strict security posture, access permissions are bound directly at the **Resource Group Scope** rather than the broad Subscription scope. This isolates teams to their respective functional workspaces and protects production systems from unauthorized modifications.

## 2. Multi-Team Role Mapping Matrix

| Simulated User Group | Target Resource Group Scope | Assigned Azure Built-in Role | Access Scope Justification & Rationale |
| :--- | :--- | :--- | :--- |
| **Dev-Engineers** | `mtt-webapp-dev-westus-rg-01` | **Contributor** | Grants full authority to create, modify, and terminate testing resources without allowing access to billing policies or production networks. |
| **Prod-Ops-Team** | `mtt-webapp-prod-westus-rg-01` | **Contributor** | Enforces operations control over live systems. Restricted completely from altering development configurations to isolate environments. |
| **IT-Auditors** | *Subscription Level* / Both RGs | **Reader** | Grants visibility across all resources to analyze operational metrics and compliance settings, with a strict lock blocking any creation or deletion actions. |

---

## 3. Resource Lifecycle Management Test (Task 6)
To verify unified lifecycle tracking, a bulk cleanup test was performed:
* **Action:** Executed bulk deletion on the temporary development group: `az group delete --name mtt-webapp-dev-westus-rg-01 --yes`
* **Result:** The virtual machines, networks, and disks inside the container were safely terminated and destroyed simultaneously. This proves that anchoring assets within an isolated resource group guarantees clean, zero-leak resource teardowns.