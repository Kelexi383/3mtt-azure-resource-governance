# Azure Resource Organization & Cloud Governance Framework

## 📌 Project Overview
This repository documents the implementation of a scalable cloud governance architecture within Microsoft Azure. This project establishes enterprise-level resource hierarchy, unified naming conventions, structured tagging schemas, and Role-Based Access Control (RBAC) security boundaries across separate Development (Dev) and Production (Prod) environments.

---

## 🏛️ 1. Global Architectural Hierarchy
To balance security boundaries with billing transparency, resources are organized according to Azure’s standard four-tier governance hierarchy:
1. **Management Groups:** (Root container for enterprise policy alignment).
2. **Subscriptions:** Used as distinct billing and environmental boundaries.
3. **Resource Groups:** Used as logical lifecycle boundaries for related assets.
4. **Resources:** The actual provisioned services (VMs, Storage, VNet).

---

## 🏷️ 2. Enterprise Naming Convention Strategy
To prevent resource clutter and ensure rapid identification, a token-based, lowercase, hyphen-delimited naming convention was designed:

**Formula:** `[provider]-[project/app]-[environment]-[region]-[resource-type-abbreviation]-[index]`

### Core Abbreviation Standard:
* **Resource Group:** `rg` | **Virtual Machine:** `vm` | **Storage Account:** `st` (no hyphens) | **Virtual Network:** `vnet`

### Examples in Action:
* **Production Resource Group:** `mtt-webapp-prod-westus-rg-01`
* **Development Storage Account:** `mttwebappdevwestusst01` *(Note: Storage accounts must be globally unique, alphanumeric only, and lowercase).*
* **Production Virtual Machine:** `mtt-webapp-prod-westus-vm-01`

---

## 📊 3. Automated Metadata Tagging Schema
Every deployed resource inherits a mandatory metadata tagging matrix to streamline automated cost allocation, billing reports, and owner accountability:

| Tag Key | Example Value (Dev) | Example Value (Prod) | Business Justification / Purpose |
| :--- | :--- | :--- | :--- |
| `Environment` | `development` | `production` | Isolates testing costs from live application revenue spend. |
| `Project` | `3mtt-labs` | `3mtt-labs` | Identifies the specific application or class module budget. |
| `Owner` | `cloud-team-dev` | `cloud-team-prod` | Escalation point for technical support and maintenance alerts. |
| `CostCenter` | `cc-4401` | `cc-9902` | Allows the accounting team to map infrastructure bills to departments. |

---

## 🚀 4. Automated CLI Environment Provisioning
The baseline environment structure was automated via the Azure CLI to demonstrate infrastructure repeatability. The script file can be examined under [`templates/deploy-governance.azcli`](./templates/deploy-governance.azcli).
