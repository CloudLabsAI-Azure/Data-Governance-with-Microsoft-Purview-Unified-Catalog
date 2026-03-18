## Lab 3: Connect Databricks Unity Catalog to Purview (60 min)

### Objective
Register the Databricks workspace, configure the Unity Catalog connector, scan all catalogs/schemas/tables, and validate assets in the Unified Catalog.

---

### Task 1: Register Databricks Workspace (10 min)

1. Go to **Data Map** → **Sources** → click **Register**
2. Select **Azure Databricks** from the source type list
3. Configure:
   - **Name**: `Contoso-Databricks`
   - **Azure subscription**: select your subscription
   - **Databricks workspace**: `dbw-purview-{deploymentId}`
   - **Collection**: select `Databricks Sources`
4. Click **Register**
5. Verify the source appears under `Databricks Sources` in the data map

**Expected Result**: Databricks workspace registered in Purview under the `Databricks Sources` collection.

---

### Task 2: Configure Unity Catalog Connector (20 min)

1. On the `Contoso-Databricks` source, click **New Scan** → this opens the scan configuration
2. Before configuring the scan, set up authentication:

   **Option A: Service Principal (recommended for CloudLabs)**
   - Go to **Management** → **Credentials** → **+ New**
   - **Name**: `Databricks-SP-Credential`
   - **Authentication method**: Service Principal
   - **Tenant ID**: auto-populated
   - **Service principal client ID**: (from CloudLabs parameters)
   - **Key Vault connection**: select `kv-purview-{deploymentId}`
   - **Secret name**: `databricks-sp-secret`
   - Click **Create**

   **Option B: Personal Access Token (PAT)**
   - Open **Databricks workspace** in a new tab: `https://adb-{workspaceId}.azuredatabricks.net`
   - Go to **User Settings** → **Developer** → **Access Tokens**
   - Click **Generate New Token**
     - Comment: `purview-scan`
     - Lifetime: `90 days`
   - Copy the token
   - In Purview **Management** → **Credentials** → **+ New**:
     - **Name**: `Databricks-PAT-Credential`
     - **Authentication method**: Access Token
     - Store token in Key Vault secret: `databricks-pat`
   - Click **Create**

3. In the Databricks workspace, verify Unity Catalog is active:
   - Go to **Catalog** in the left sidebar
   - Confirm `contoso_catalog` exists with schemas: `sales`, `hr`
   - Confirm tables exist under each schema

**Expected Result**: Credential created for Databricks scanning. Unity Catalog verified with `contoso_catalog` containing `sales` and `hr` schemas.

---

### Task 3: Scan Catalogs, Schemas, and Tables (15 min)

1. Back in **Purview** → **Data Map** → **Sources** → `Contoso-Databricks`
2. Click **New Scan** and configure:
   - **Name**: `Scan-Databricks-Full`
   - **Credential**: select the credential from Task 2
   - **Integration runtime**: Azure AutoResolve
3. **Scope**: Select the entire Unity Catalog:
   - ✅ `contoso_catalog`
     - ✅ `sales` schema
     - ✅ `hr` schema
4. **Scan rule set**: Use system default **Databricks** rules (includes classification)
5. **Scan trigger**: select **Once**
6. Click **Save and Run**
7. Monitor scan progress (typically 3-5 minutes for this data size)
8. After completion, review discovered assets:

   | Catalog | Schema | Tables |
   |---------|--------|--------|
   | contoso_catalog | sales | `customers`, `orders`, `products` |
   | contoso_catalog | hr | `employees` |

**Expected Result**: Scan discovers 4 tables across 2 schemas in 1 catalog. All assets appear under the `Databricks Sources` collection.

---

### Task 4: Validate Databricks Assets in Unified Catalog (15 min)

1. Go to **Unified Catalog** → **Search** (or **Data Catalog** → **Search**)
2. Search for `contoso_catalog` → verify the catalog asset appears
3. Click on `contoso_catalog.sales.customers`:
   - **Overview**: table type (Managed/External), location, format (Delta)
   - **Schema**: column names, data types
   - **Classifications**: check if PII classifications were applied
   - **Lineage**: any notebook-generated lineage (if notebooks ran)
4. Search for `contoso_catalog.hr.employees`:
   - Verify PII classifications: **SSN**, **Email**, **Phone**, **Person Name**
   - These should be auto-detected from column content
5. Compare the same `customers` data across platforms:
   - Search for `customers` → you should see results from:
     - Fabric Lakehouse: `customers` table
     - Fabric Warehouse: `dim_customers` table
     - Databricks: `contoso_catalog.sales.customers` table
   - This demonstrates **unified discovery** across multi-cloud data sources

**Expected Result**: All Databricks Unity Catalog assets visible in Purview. PII classifications auto-applied on `employees` table. Same data discoverable across Fabric + Databricks in unified search.

---
