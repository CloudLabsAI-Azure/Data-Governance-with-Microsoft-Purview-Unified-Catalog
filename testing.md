# Day 1 — Lab 4: Classification, Lineage & Cross-Platform Governance

**Duration**: 60 min

---

## Overview

In Labs 2 and 3, you connected Fabric and Databricks to Purview and discovered schemas and tables. But you may have noticed:
- **No classifications** appeared on any columns
- **No lineage** (data flow diagrams) appeared on any assets

This is because Fabric and Databricks scans only capture **structural metadata** (column names, types). Purview cannot read the actual data values from these sources.

In this lab you will:
1. **Upload a PII-rich CSV to Azure Storage** → Purview scans it and **auto-classifies** SSNs, emails, and phone numbers
2. **Manually classify** Fabric and Databricks columns (the standard approach for these sources)
3. **Create a Fabric Data Pipeline** → Purview captures **data lineage** showing how data moves from Lakehouse to Warehouse

After this lab, all three core Purview features will be visible: **discovery, classification, and lineage**.

---

## Task 1: Upload Employee Data to ADLS Gen2 and Scan (20 min)

> Azure Data Lake Storage Gen2 (ADLS) is one of the source types where Purview **reads actual data values** during scanning. This enables automatic PII detection using 200+ built-in classification rules.

**Step 1: Create the Employee CSV File**

1. On your lab machine, open **Notepad**
2. Copy and paste the following data exactly:

```csv
employee_id,full_name,email,ssn,date_of_birth,department,salary,hire_date,phone,address
E001,John Smith,john.smith@contoso.com,123-45-6789,1985-03-15,Engineering,95000,2020-01-10,555-012-3456,123 Main St Seattle WA 98101
E002,Jane Doe,jane.doe@contoso.com,234-56-7890,1990-07-22,Marketing,82000,2021-03-15,555-023-4567,456 Oak Ave Portland OR 97201
E003,Carlos Garcia,carlos.garcia@contoso.com,345-67-8901,1988-11-30,Sales,78000,2019-06-01,555-034-5678,789 Pine Rd Austin TX 78701
E004,Priya Patel,priya.patel@contoso.com,456-78-9012,1992-04-18,Engineering,105000,2022-01-20,555-045-6789,321 Elm St San Jose CA 95101
E005,Wei Zhang,wei.zhang@contoso.com,567-89-0123,1987-09-05,Finance,88000,2020-08-15,555-056-7890,654 Cedar Ln Chicago IL 60601
E006,Sarah Johnson,sarah.johnson@contoso.com,678-90-1234,1993-12-10,Marketing,76000,2021-11-01,555-067-8901,987 Birch Dr Miami FL 33101
E007,Ahmed Hassan,ahmed.hassan@contoso.com,789-01-2345,1986-04-25,Engineering,110000,2018-04-01,555-078-9012,147 Maple Way Denver CO 80201
E008,Maria Santos,maria.santos@contoso.com,890-12-3456,1991-08-14,Sales,72000,2022-05-20,555-089-0123,258 Walnut Ct Boston MA 02101
E009,David Kim,david.kim@contoso.com,901-23-4567,1989-01-30,Finance,92000,2019-09-15,555-090-1234,369 Spruce Pl Atlanta GA 30301
E010,Lisa Brown,lisa.brown@contoso.com,012-34-5678,1994-06-08,HR,68000,2023-02-01,555-001-2345,741 Poplar Rd Phoenix AZ 85001
```

3. Click **File** → **Save As**:
   - **File name**: `employees.csv`
   - **Save as type**: All Files (*.*)
   - **Encoding**: UTF-8
   - Save to your **Desktop**

**Step 2: Upload to Azure Storage**

4. Go to the **Azure portal** (`https://portal.azure.com`)
5. In the search bar, type `adlspurview` → click on your storage account (`adlspurview{deploymentId}`)
6. In the left menu, click **Containers**
7. Click on the `raw` container
   > If the `raw` container doesn't exist: click **+ Container** → Name: `raw` → click **Create** → then click into it
8. Click **Upload** (top toolbar)
9. Click **Browse for files** → select `employees.csv` from your Desktop
10. Click **Upload**
11. Verify `employees.csv` appears in the container file list

**Step 3: Register ADLS Gen2 as a Data Source in Purview**

12. Switch to the **Purview portal** (`https://purview.microsoft.com`)
13. Click **Data Map** → **Data sources** → **Register**
14. Search for and select **Azure Data Lake Storage Gen2** → click **Continue**
15. Configure:
    - **Name**: `Contoso-ADLS`
    - **Azure subscription**: select your subscription
    - **Storage account name**: `adlspurview{deploymentId}`
    - **Collection**: select `Shared Assets` (the sub-collection from Lab 1)
16. Click **Register**
17. Verify `Contoso-ADLS` appears under `Shared Assets` in the data map

**Step 4: Scan the Storage Account**

18. Click on `Contoso-ADLS` → click **+ New scan**
19. Configure:
    - **Name**: `Scan-ADLS-Raw`
    - **Credential**: **Microsoft Purview MSI (system)** (default)
    - **Integration runtime**: Azure AutoResolveIntegrationRuntime
20. Click **Continue** → **Scope**: expand the tree → check the box next to `raw` container
    > Only scan the `raw` container — this is where your employees.csv lives
21. Click **Continue** → **Scan rule set**: select **System default** (AdlsGen2)
    > The system default rule set includes all 200+ built-in classification rules — this is what detects SSNs, emails, etc.
22. **Scan trigger**: select **Once**
23. Click **Continue** → review → **Save and Run**

**Step 5: Wait for Scan and Review Auto-Classifications**

24. Go to **Data sources** → `Contoso-ADLS` → **Recent scans**
25. Wait for **Completed** status (typically 2-5 minutes)
26. Now go to **Data Catalog** → search for `employees`
27. Click on the `employees.csv` asset (source: Azure Data Lake Storage Gen2)
28. Click the **Schema** tab
29. Review the **auto-detected classifications**:

    | Column | Expected Classification | Detection Method |
    |--------|------------------------|-----------------|
    | `full_name` | **Person's Name** | Machine Learning model |
    | `email` | **Email Address** | Regex pattern matching |
    | `ssn` | **U.S. Social Security Number (SSN)** | Regex: `XXX-XX-XXXX` |
    | `date_of_birth` | **Date of Birth** | ML + keyword detection |
    | `phone` | **U.S. Phone Number** | Regex pattern matching |
    | `address` | **U.S. Street Address** | Machine Learning model |
    | `employee_id` | *(no classification)* | Not PII |
    | `department` | *(no classification)* | Not PII |
    | `salary` | *(no classification)* | Not PII |
    | `hire_date` | *(no classification)* | Not PII |

    > **Note**: Not all classifications may appear — Purview requires a minimum 60% confidence threshold. If a column doesn't get classified, it means the sample data didn't meet the threshold. The columns most likely to be classified are `ssn`, `email`, and `full_name`.

30. Click on a classified column (e.g., `ssn`) → note the classification details:
    - Classification name
    - Classification type (System/built-in)
    - Confidence score

**Expected Result**: `employees.csv` scanned in ADLS Gen2. Multiple PII classifications auto-detected on columns containing SSNs, emails, names, phone numbers, and addresses. No manual labeling was needed — Purview found them automatically.

---

## Task 2: Manually Classify Fabric and Databricks Assets (15 min)

> For source types where auto-classification is not supported (Fabric, Databricks Unity Catalog), governance teams apply classifications **manually**. This is standard practice in enterprise data governance.

**Step 1: Classify Fabric Lakehouse Columns**

1. In the **Data Catalog**, search for `dimension_customer`
2. Click on the **Lakehouse Table** result (source: Microsoft Fabric)
3. Click the **Schema** tab — note that **no classifications** appear (this is expected for Fabric)
4. Click the **Edit** button (pencil icon) at the top of the schema section
   > If you don't see Edit, verify you have **Data Curator** role on the `Fabric Sources` collection (Lab 1)
5. On the `Customer` column row, click the **Classification** dropdown → search and select **Person's Name**
6. On the `Postal Code` column row, click **Classification** → search and select **U.S. Zip Code**
7. Click **Save**
8. Verify the classification tags now appear on those columns

**Step 2: Classify Databricks Columns**

9. Search for `customer` → click the result from the Databricks `samples.tpch` schema
10. Click the **Schema** tab → click **Edit**
11. On the `c_name` column → add classification: **Person's Name**
12. On the `c_phone` column → add classification: **U.S. Phone Number**
13. Click **Save**

**Step 3: Compare Auto vs Manual Classification**

14. Now compare the three customer/employee assets side by side:

    | Asset | Source | Classification Method | What Was Classified |
    |-------|--------|----------------------|-------------------|
    | `employees.csv` | ADLS Gen2 | **Automatic** — Purview read the data | SSN, Email, Name, Phone, DOB, Address |
    | `dimension_customer` | Fabric Lakehouse | **Manual** — you added labels | Person's Name, Zip Code |
    | `tpch.customer` | Databricks | **Manual** — you added labels | Person's Name, Phone |

15. Key governance takeaway:
    - **Auto-classification** works for ADLS, Azure SQL, Blob Storage — sources where Purview can sample row data
    - **Manual classification** is required for Fabric, Databricks UC — sources where Purview only reads metadata
    - In enterprise environments, you use **both**: auto for data lakes and databases, manual for cloud analytics platforms
    - Both methods produce the **same classification labels** in the catalog — consumers don't see the difference

**Expected Result**: Manual classifications applied to Fabric and Databricks columns. Student understands when auto vs manual classification applies.

---

## Task 3: Create a Fabric Pipeline and View Lineage (25 min)

> Lineage in Purview tracks **data movement** — when data flows from one asset to another via a pipeline, dataflow, or copy activity. Without data movement, there is no lineage to show.
>
> In this task, you'll create a simple Data Pipeline in Fabric that copies data from the Lakehouse to the Warehouse. After re-scanning, Purview will capture this data flow as a lineage diagram.

**Step 1: Create a Data Pipeline in Fabric**

1. Go to the **Fabric portal** (`https://app.fabric.microsoft.com`)
2. Navigate to your workspace (`Purview-Lab-WS`)
3. Click **+ New item** → select **Data pipeline**
4. **Name**: `Customer-ETL-Pipeline` → click **Create**
5. You should now be in the Pipeline canvas (visual editor)

**Step 2: Add a Copy Activity**

6. In the pipeline canvas, click **Copy data** (from the activity toolbar, or click **Add pipeline activity** → **Copy data**)
7. A Copy data activity appears on the canvas — click on it to configure

**Step 3: Configure the Source**

8. Click the **Source** tab (bottom panel)
9. Click **+ New** next to **Connection**
10. Select **Microsoft Fabric Lakehouse** → click **Connect**
    > If prompted for workspace, select `Purview-Lab-WS`
11. Select **Lakehouse**: `Purview-Lakehouse`
12. Click **OK** / **Connect**
13. Under **Table**, browse and select: `dimension_customer`
    > This is the WWI sample table from Lab 2 — it has customer data like Customer Key, Customer Name, Postal Code, Category, Buying Group, etc.

**Step 4: Configure the Destination**

14. Click the **Destination** tab
15. Click **+ New** next to **Connection**
16. Select **Microsoft Fabric Warehouse** → click **Connect**
17. Select **Warehouse**: `Purview-Warehouse`
18. Click **OK** / **Connect**
19. Under **Table option**, select **Auto create table**
20. Enter **Table name**: `stg_customers`
    > This creates a new staging table in the Warehouse with the same schema as dimension_customer

**Step 5: Run the Pipeline**

21. Click **Run** (play button) in the toolbar → click **Save and run** if prompted
22. Wait for the pipeline to complete (typically 1-2 minutes)
23. Verify **Status: Succeeded**
    > If it fails — check that the Lakehouse and Warehouse still have data, and that you have contributor access to the workspace

**Step 6: Verify the Data Moved**

24. Go back to the workspace → click on **Purview-Warehouse**
25. In the Explorer pane, expand **dbo** → **Tables**
26. You should see `stg_customers` listed as a new table
27. Right-click → **Select TOP 1000 rows** → verify the customer data appears
    > This is the same WWI customer data from the Lakehouse, now copied to the Warehouse

**Step 7: Re-Scan Fabric to Capture Lineage**

28. Switch to **Purview portal** → **Data Map** → **Data sources** → click `Purview-Fabric`
29. Click **+ New scan** (or re-run the existing scan):
    - **Name**: `Scan-Fabric-Lineage`
    - **Credential**: Microsoft Purview MSI (system)
    - Scope: `Purview-Lab-WS` workspace
    - Scan rule set: System default
    - Trigger: Once
30. Click **Save and Run**
31. Wait for **Completed** status (3-5 minutes)

**Step 8: View the Lineage Diagram**

32. Go to **Data Catalog** → search for `stg_customers`
33. Click on the **stg_customers** asset (in the Warehouse)
34. Click the **Lineage** tab
35. You should see a lineage diagram:

    ```
    ┌─────────────────────┐     ┌──────────────────────┐     ┌─────────────────────┐
    │  dimension_customer  │ ──→ │ Customer-ETL-Pipeline │ ──→ │   stg_customers     │
    │  (Lakehouse Table)   │     │  (Data Pipeline)      │     │  (Warehouse Table)  │
    └─────────────────────┘     └──────────────────────┘     └─────────────────────┘
    ```

    - **Left node**: `dimension_customer` — the source table in the Lakehouse
    - **Middle node**: `Customer-ETL-Pipeline` — the pipeline that moved the data
    - **Right node**: `stg_customers` — the destination table in the Warehouse

36. Click on each node to see details:
    - Click the **source node** → links to the Lakehouse table asset
    - Click the **pipeline node** → shows the pipeline name and workspace
    - Click the **destination node** → links to the Warehouse table asset

37. Go back → search for `dimension_customer` → click the Lakehouse table → **Lineage** tab
38. You should see the same lineage from the source perspective (arrow going OUT to the pipeline)

    > **Note**: If lineage doesn't appear immediately after the scan, wait 10-15 minutes. Purview processes lineage asynchronously and it may take a short delay to render.

**Step 9: Compare Lineage Across Sources**

39. Now check lineage on a Databricks asset: search for `tpch.customer` → **Lineage** tab
    - This shows **"Not available"** — expected, because no data was moved to/from this table
40. Check lineage on the **Semantic model** (Power BI Dataset): search for `Purview-Lakehouse` → click the Power BI Dataset → **Lineage** tab
    - This may show a connection from the SQL analytics endpoint to the Semantic model

41. Summary of lineage across all sources:

    | Asset | Lineage Visible? | Why? |
    |-------|-----------------|------|
    | `dimension_customer` (Lakehouse) | ✅ **Yes** — arrow to Pipeline | Pipeline copies data FROM this table |
    | `stg_customers` (Warehouse) | ✅ **Yes** — arrow from Pipeline | Pipeline copies data TO this table |
    | `Customer-ETL-Pipeline` | ✅ **Yes** — connects source to destination | Pipeline is the data movement activity |
    | Semantic model (Power BI Dataset) | ✅ May show SQL endpoint → Dataset link | Fabric tracks item-level connections |
    | `tpch.customer` (Databricks) | ❌ Not available | No data movement — read-only `samples` catalog |

42. Key governance takeaway: **Lineage requires data movement.** Purview automatically captures it when you use Fabric Pipelines, Dataflows, or Databricks notebooks that write data. No lineage appears for static/read-only data.

**Expected Result**: Pipeline created and ran successfully. `stg_customers` table created in Warehouse. Re-scan captured lineage. Lineage diagram visible showing Lakehouse → Pipeline → Warehouse data flow.

---

## Lab 4 Summary

| Task | What You Did | Feature Demonstrated | Time |
|------|-------------|---------------------|------|
| 1 | Uploaded employees.csv to ADLS Gen2, registered and scanned | **Auto-classification** — SSN, Email, Phone, Name detected | 20 min |
| 2 | Manually classified Fabric and Databricks customer columns | **Manual classification** — same labels, different method | 15 min |
| 3 | Created Fabric Pipeline (Lakehouse → Warehouse), re-scanned | **Data lineage** — visual data flow diagram | 25 min |
| | **Total** | | **60 min** |

---

## After Day 1: What You've Built

| Source | Assets in Catalog | Classification | Lineage |
|--------|------------------|---------------|---------|
| **Fabric Lakehouse** | dimension_customer, fact_sale, dimension_city, etc. | ✅ Manual (Person's Name, Zip Code) | ✅ Source of Pipeline lineage |
| **Fabric Warehouse** | Purview-Warehouse + stg_customers | — | ✅ Destination of Pipeline lineage |
| **Fabric Semantic Model** | Power BI Dataset with full schema | — | ✅ SQL endpoint → Dataset |
| **Databricks** | samples.tpch (8 tables), samples.nyctaxi | ✅ Manual (Person's Name, Phone) | ❌ Read-only catalog |
| **ADLS Gen2** | employees.csv | ✅ **Auto** (SSN, Email, Phone, Name, DOB, Address) | — |

**All three Purview core capabilities are now visible:**
- **Discovery**: Assets from Fabric, Databricks, and ADLS searchable in one catalog
- **Classification**: Auto (ADLS) + Manual (Fabric, Databricks) — consistent labels across platforms
- **Lineage**: Fabric Pipeline data flow tracked and visualized

**Next**: Day 2 — Unified Catalog, Discovery & Data Products
