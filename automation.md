# Purview Workshop — Pre-Created Resources & Automation

All resources below are deployed automatically by CloudLabs before participants start. The `{id}` placeholder is the unique CloudLabs deployment ID.

---

## Layer 1: Azure Resources (ARM Template)

Deployed by: `deploy-day1.json`

| # | Resource | Name Pattern | Key Config |
|---|----------|-------------|------------|
| 1 | NSG (default) | `nsg-purview-{id}` | Empty rules |
| 2 | NSG (Databricks) | `nsg-dbw-{id}` | Empty rules |
| 3 | VNet | `vnet-purview-{id}` | `10.10.0.0/16`, 4 subnets |
| | - Subnet: `default` | | `10.10.1.0/24` |
| | - Subnet: `purview-subnet` | | `10.10.2.0/24` |
| | - Subnet: `databricks-public` | | `10.10.3.0/24` (delegated to Databricks) |
| | - Subnet: `databricks-private` | | `10.10.4.0/24` (delegated to Databricks) |
| 4 | ADLS Gen2 | `adlspurview{id}` | HNS enabled, Standard_LRS, TLS 1.2 |
| | - Container: `raw` | | No public access |
| | - Container: `curated` | | No public access |
| | - Container: `sandbox` | | No public access |
| 5 | Azure Databricks | `dbw-purview-{id}` | Premium tier, VNet-injected |
| | - Managed RG | `databricks-rg-{id}` | Auto-created by Databricks |
| 6 | Key Vault | `kv-purview-{id}` | RBAC auth, soft delete 7 days |
| 7 | Microsoft Purview | `purview-{id}` | System-assigned MSI, public network |
| | - Managed RG | `managed-purview-{id}` | Auto-created by Purview |

**Total ARM resources**: 9 (+ 2 managed RGs auto-created)

---

## Layer 2: Fabric Resources

Deployed by: `scripts/seed-fabric-workspace.ps1`

| # | Resource | Name | Contents |
|---|----------|------|----------|
| 8 | Fabric Workspace | `ws-purview-{id}` | Container for all Fabric items |
| 9 | Lakehouse | `SalesLakehouse` | In workspace |
| | - Table: `customers` | | 10 rows (customer_id, name, email, phone, city, state) |
| | - Table: `orders` | | 12 rows (order_id, customer_id, product_id, dates, amounts) |
| | - Table: `products` | | 8 rows (product_id, name, category, brand, price) |
| | - Table: `employees` | | 5 rows (PII: SSN, email, phone, DOB, salary) |
| 10 | Warehouse | `SalesWarehouse` | In workspace (SQL endpoint) |
| | - Table: `dim_customers` | | 5 rows (mirrors Lakehouse customers) |
| | - Table: `dim_products` | | 5 rows (mirrors products) |
| | - Table: `fact_orders` | | 8 rows (order transactions) |
| | - View: `vw_sales_summary` | | Joins fact_orders + dim_customers + dim_products |
| 11 | Semantic Model | `Sales Analytics` | Built over Warehouse tables (MANUAL) |

**RBAC**: Purview MSI gets **Storage Blob Data Reader** on ADLS Gen2

---

## Layer 3: Databricks Resources

Deployed by: `scripts/seed-databricks-unity-catalog.ps1`

| # | Resource | Name | Contents |
|---|----------|------|----------|
| 12 | Unity Catalog Metastore | `purview-metastore-{id}` | Storage root in `sandbox` container |
| 13 | Catalog | `contoso_catalog` | Top-level catalog |
| 14 | Schema: sales | `contoso_catalog.sales` | "Sales and commerce data" |
| | - Table: `customers` | | 10 rows (same data as Fabric Lakehouse) |
| | - Table: `orders` | | 12 rows (same data as Fabric Lakehouse) |
| | - Table: `products` | | 5 rows (same data) |
| 15 | Schema: hr | `contoso_catalog.hr` | "Human resources and employee data" |
| | - Table: `employees` | | 5 rows (PII: SSN, email, phone, DOB, salary) |
| 16 | SQL Warehouse | `purview-seed-warehouse` | 2X-Small PRO, serverless, auto-stop 15 min (stopped after seeding) |

---

## Layer 4: Licenses Needed (Not Deployable)

| # | License | Purpose | How to Get |
|---|---------|---------|------------|
| 17 | Purview Data Governance | Unified Catalog, Domains, Glossary, Data Products | Trial activation in Purview portal, or Fabric F64+ bundle |
| 18 | Microsoft Fabric capacity | Workspace, Lakehouse, Warehouse, Semantic Models | F64+ capacity or Fabric trial (60-day free) |
| 19 | Databricks Premium | Unity Catalog support | Deployed via ARM (Premium SKU) |

---

## Summary Count

| Category | Count |
|----------|-------|
| Azure resources (ARM) | 9 resources + 2 managed RGs |
| Fabric items | 3 (Workspace + Lakehouse + Warehouse) |
| Lakehouse tables | 4 (customers, orders, products, employees) |
| Warehouse tables | 3 + 1 view |
| Databricks catalog objects | 1 metastore + 1 catalog + 2 schemas + 4 tables + 1 SQL warehouse |
| RBAC assignments | 1 (Purview MSI → Storage) |
| Manual post-deploy steps | 3 (Warehouse SQL seed, Semantic Model, Purview trial) |
| **Total pre-created items** | **~30** |

---

## 3 Things Still Manual

1. **Warehouse SQL seed** — Run `warehouse-seed.sql` against Fabric SQL analytics endpoint (script saves the file but can't connect via REST)
2. **Semantic Model "Sales Analytics"** — Must be created in Fabric portal UI (no REST API for this)
3. **Purview Data Governance trial** — Activated in `purview.microsoft.com` (license toggle)

---

## Deployment Order

```
deploy-day1.ps1
├── 1. ARM template (deploy-day1.json) → 9 Azure resources
├── 2. seed-fabric-workspace.ps1 → Workspace + Lakehouse + Warehouse + data
├── 3. seed-databricks-unity-catalog.ps1 → Metastore + Catalog + Schemas + Tables
└── 4. Manual: Warehouse SQL + Semantic Model + Purview trial
```

## Files

| File | Purpose |
|------|---------|
| `deploy-day1.json` | ARM template (9 resources) |
| `deploy-day1.parameters.json` | ARM parameters |
| `deploy-day1.ps1` | Orchestrator script |
| `scripts/seed-fabric-workspace.ps1` | Fabric workspace + Lakehouse + Warehouse |
| `scripts/seed-databricks-unity-catalog.ps1` | Unity Catalog + schemas + tables |
| `scripts/seed-day1-data.ps1` | Backup ADLS/SQL seed script |
| `day1/day1-lab-guide.md` | Lab guide (4 labs, 14 tasks, 220 min) |
