# Lab 4: Foundational Metadata, Classification & Lineage (50 min)

### Objective
Run comprehensive scans across both platforms, apply classifications, and review cross-platform technical lineage.

---

### Task 1: Run Initial Scans Across Fabric and Databricks (15 min)

1. Verify both scans from Labs 2 and 3 completed successfully:
   - Go to **Data Map** → **Sources**
   - Click on `Contoso-Fabric` → **Scans** tab → status should be **Completed**
   - Click on `Contoso-Databricks` → **Scans** tab → status should be **Completed**
2. If any scan failed:
   - Click on the failed scan → review **Error details**
   - Common fixes:
     - **Authentication error**: verify credential permissions
     - **Timeout**: re-run the scan
     - **Missing permissions**: ensure Purview MSI has access
   - Re-run the failed scan
3. Review the combined **Data Map** view:
   - Go to **Data Map** → **Sources** → **View map**
   - Observe both sources under their collections
   - Note total asset counts per source
4. Go to **Data Estate Insights** → **Assets**:
   - Total assets discovered across all sources
   - Breakdown by source type (Fabric vs Databricks)
   - Scan success rates

**Expected Result**: Both scans completed. Data map shows 12+ assets across 2 source types. Insights dashboard reflects combined asset metrics.

---

### Task 2: Apply Built-in Classifications (20 min)

1. Go to **Data Catalog** (or **Unified Catalog**) → Search for `employees`
2. You should see employee data from multiple sources:
   - Fabric Lakehouse: `employees` Delta table
   - Databricks: `contoso_catalog.hr.employees`
3. Click on the **Fabric Lakehouse** `employees` table:
   - Go to **Schema** tab
   - Review auto-applied classifications:

     | Column | Expected Classification |
     |--------|----------------------|
     | email | Email Address |
     | ssn | US Social Security Number |
     | phone | Phone Number |
     | full_name | Person's Name |
     | date_of_birth | Date of Birth |
     | salary | N/A (numeric, not classified by default) |

4. Click on the **Databricks** `contoso_catalog.hr.employees` table:
   - Compare classifications — should match the Fabric version
5. If any expected classification is missing:
   - Go to **Data Map** → **Scan rule sets**
   - Click on the scan rule used → verify **System classifications** are enabled
   - Key rules to verify: `US Social Security Number`, `Email Address`, `Person's Name`, `Phone Number`
   - If needed, **re-run the scan** with updated rules

6. Review classification summary:
   - Go to **Data Estate Insights** → **Classifications**
   - View:
     - Which classifications were detected
     - How many assets per classification
     - Cross-source classification distribution

**Expected Result**: PII classifications (SSN, Email, Phone, Name) auto-applied on employee data from both Fabric and Databricks. Classification insights show cross-platform PII distribution.

---

### Task 3: Review Technical Lineage Across Platforms (15 min)

1. **Fabric Lineage Chain**:
   - Search for `vw_sales_summary` (Fabric Warehouse view) → click on it
   - Go to **Lineage** tab
   - Observe the lineage chain:
     ```
     Lakehouse tables → Warehouse tables → vw_sales_summary view → Semantic Model
     ```
   - Click through each node to understand the data flow

2. **Databricks Lineage** (if notebooks ran):
   - Search for `contoso_catalog.sales.orders` → click on it
   - Go to **Lineage** tab
   - If a Databricks notebook processed this table, lineage shows:
     ```
     Source data → Notebook transformation → orders table
     ```
   > **Note**: Databricks lineage requires notebooks to have run with Unity Catalog lineage tracking enabled. If no lineage shows, this is expected — lineage will be generated in Day 3 when we run transformation notebooks.

3. **Cross-platform comparison**:
   - Search for `customers` → view all 3 versions:
     - Fabric Lakehouse `customers`
     - Fabric Warehouse `dim_customers`
     - Databricks `contoso_catalog.sales.customers`
   - For each, check the **Lineage** tab
   - Note: cross-platform lineage (Databricks → Fabric) requires explicit data movement — this will be configured in Day 3

4. **Lineage Insights**:
   - Go to **Data Estate Insights** → **Lineage** (if available)
   - Review:
     - Assets with lineage vs without
     - Most connected assets
     - Lineage depth

**Expected Result**: Fabric lineage chain visible from Lakehouse → Warehouse → View → Semantic Model. Databricks lineage visible if notebooks ran. Cross-platform lineage noted as a Day 3 goal.

---
