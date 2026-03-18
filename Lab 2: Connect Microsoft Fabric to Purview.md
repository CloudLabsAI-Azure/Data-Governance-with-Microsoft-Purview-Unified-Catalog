## Lab 2: Connect Microsoft Fabric to Purview (60 min)

### Objective
Register Fabric as a data source in Purview, connect workspace assets, scan Lakehouse and Warehouse, and discover Semantic Models in the Unified Catalog.

---

### Task 1: Register Microsoft Fabric as a Data Source (10 min)

1. Go to **Data Map** → **Sources** → click **Register**
2. Select **Microsoft Fabric** from the source type list
   > If "Microsoft Fabric" is not listed, select **Power BI** (Fabric sources may appear under Power BI in some tenants)
3. Configure:
   - **Name**: `Contoso-Fabric`
   - **Tenant**: your Azure AD tenant (auto-populated)
   - **Collection**: select `Fabric Sources`
4. Click **Register**
5. Verify the source appears under `Fabric Sources` in the data map

**Expected Result**: Microsoft Fabric registered as a source in Purview under the `Fabric Sources` collection.

---

### Task 2: Configure Fabric Workspace Connection (15 min)

1. Open a new browser tab → go to **app.fabric.microsoft.com**
2. Navigate to the workspace `ws-purview-{deploymentId}`
3. In Fabric workspace settings:
   - Click **Settings** (gear icon) → **Governance and Insights**
   - Verify **Microsoft Purview** integration is enabled
   - If not, toggle **Enable Microsoft Purview** → **ON**
   - Select your Purview account: `purview-{deploymentId}`
   - Click **Save**
4. Back in the **Purview portal** → **Data Map** → **Sources** → `Contoso-Fabric`
5. Verify the workspace connection shows as **Connected**
6. Note the workspace items available:
   - Lakehouse(s)
   - Warehouse(s)
   - Semantic Model(s)
   - Notebooks (metadata only)

**Expected Result**: Fabric workspace connected to Purview. Workspace items visible in the source details.

---

### Task 3: Scan Fabric Lakehouse and Warehouse (20 min)

1. In **Data Map** → **Sources** → `Contoso-Fabric`, click **New Scan**
2. Configure the scan:
   - **Name**: `Scan-Fabric-Full`
   - **Integration runtime**: Azure AutoResolve
   - **Credential**: Delegated authentication (uses your signed-in identity)
3. **Scope**: Expand the workspace and select:
   - ✅ Lakehouse: `SalesLakehouse`
   - ✅ Warehouse: `SalesWarehouse`
   - ✅ Semantic Models
4. **Scan rule set**: Use system default **Fabric** scan rules
5. **Scan trigger**: select **Once**
6. Click **Save and Run**
7. Monitor scan progress:
   - Go to **Scans** tab on the Fabric source
   - Wait for completion (typically 5-8 minutes)
8. After completion, review discovered assets:

   | Asset Type | Expected Assets |
   |-----------|----------------|
   | Lakehouse Tables | `customers`, `orders`, `products`, `employees` (Delta) |
   | Warehouse Tables | `dim_customers`, `fact_orders`, `dim_products` |
   | Warehouse Views | `vw_sales_summary` |
   | Semantic Models | `Sales Analytics` |

**Expected Result**: Scan discovers 8+ Fabric assets. Lakehouse Delta tables, Warehouse tables/views, and Semantic Model all visible in Purview.

---

### Task 4: Discover Fabric Semantic Models in Unified Catalog (15 min)

1. Go to **Unified Catalog** → **Search**
   > If Unified Catalog is not available, use **Data Catalog** → **Search** instead
2. Search for `Sales Analytics` → click on the Semantic Model asset
3. Review the asset detail page:
   - **Overview**: model name, workspace, last refreshed
   - **Schema**: tables and measures exposed in the model
   - **Lineage**: trace back from Semantic Model → Warehouse tables → source data
   - **Related**: linked Warehouse tables
4. Search for `dim_customers` → click on the Warehouse table
5. On the **Lineage** tab, observe:
   - Warehouse `dim_customers` ← sourced from Lakehouse `customers` (if ETL ran)
   - Semantic Model `Sales Analytics` ← consumes Warehouse tables
6. Browse by **Domain**:
   - Go to **Unified Catalog** → **Browse** → click `Sales & Commerce` domain
   - Note: assets won't be assigned to domains yet (we'll do this in Day 2)
   - This shows where domain-based browsing will be useful

**Expected Result**: Semantic Model discoverable in Unified Catalog. Lineage shows asset relationships from Lakehouse → Warehouse → Semantic Model.

---
