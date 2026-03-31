# Day 1 — Lab 4: Classification, Lineage & Cross-Platform Governance

**Duration**: 50 min

---

## Overview

In Labs 2 and 3, you connected Fabric and Databricks to Purview and discovered schemas and tables. But you may have noticed:
- **No classifications** appeared on any columns
- **No lineage** (data flow diagrams) appeared on any assets

In this lab you will upload your own employee data into the Fabric Lakehouse, apply classifications, create a data pipeline for lineage, and compare governance features across Fabric and Databricks — all from one data set.

---

## Task 1: Run Initial Scans Across Fabric and Databricks (10 min)

> Before working with classifications and lineage, confirm that the scans from Labs 2 and 3 completed successfully and that all assets are discoverable in the catalog.

**Step 1: Verify Scan Status**

1. Go to **Purview portal** (`https://purview.microsoft.com`) → **Data Map** → **Data sources**
2. Click your Fabric source (`Purview-Fabric`) → **Recent scans** → confirm **Completed** status
3. Go back → click your Databricks source (`Purview-Databricks-UC`) → **Recent scans** → confirm **Completed** status
   > If either scan failed or is still running, re-run it before proceeding

**Step 2: Upload Employee Data to Fabric Lakehouse**

4. Go to the **Fabric portal** (`https://app.fabric.microsoft.com`)
5. Navigate to your workspace (`Purview-Lab-WS`) → click **Purview-Lakehouse**
6. In the Lakehouse Explorer, click the **Files** section (not Tables)
7. Click **Upload** → **Upload files**
8. Click **Browse** → on your lab machine, create or locate a file named `employees.csv` with this content:

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

   > **Tip**: Open Notepad → paste the CSV content → **File** → **Save As** → File name: `employees.csv` → Save as type: All Files → Encoding: UTF-8 → save to Desktop. Then upload from Desktop.

9. Once uploaded, you should see `employees.csv` in the Files section
10. Right-click `employees.csv` → select **Load to Tables** → **New table**
11. Table name: `employees` → click **Load**
12. Wait for the load to complete — the `employees` table now appears under **Tables**
13. Click on `employees` → verify the data: 10 rows with columns like full_name, email, ssn, phone, address

**Step 3: Re-Scan Fabric to Discover the New Table**

14. Switch to **Purview portal** → **Data Map** → **Data sources** → click `Purview-Fabric`
15. Click **+ New scan** (or re-run the existing scan):
    - **Name**: `Scan-Fabric-Updated`
    - **Credential**: Microsoft Purview MSI (system)
    - Scope: `Purview-Lab-WS` workspace
    - Scan rule set: System default
    - Trigger: Once
16. Click **Save and Run**
17. Wait for **Completed** status (3-5 minutes)

**Step 4: Verify All Assets in the Data Catalog**

18. Go to **Data Catalog** → search for `employees`
19. Confirm the new `employees` table appears (source: Microsoft Fabric)
20. Also search for `dimension_customer` and `fact_sale` — all existing WWI tables should still be there
21. Search for `customer` → confirm Databricks `samples.tpch.customer` also appears

**Expected Result**: Both Fabric and Databricks scans completed. Employee data uploaded and loaded as a Lakehouse table. Re-scan discovered the new `employees` table alongside existing WWI sample data and Databricks assets.

---

## Task 2: Apply Built-in Classifications (20 min)

> Purview does **not** auto-classify data during Fabric or Databricks scans. Auto-classification (data sampling with ML/regex rules) only works for sources like Azure SQL, ADLS, and Blob Storage. For Fabric and Databricks, governance teams apply classifications **manually** — this is standard practice in enterprise environments.

**Step 1: Classify the Employees Table (Fabric)**

1. In the **Data Catalog**, search for `employees`
2. Click on the **employees** Lakehouse table (source: Microsoft Fabric)
3. Click the **Schema** tab — note that **no classifications** appear (expected for Fabric)
4. Click the **Edit** button (pencil icon) at the top of the schema section
   > If you don't see Edit, verify you have **Data Curator** role on the `Fabric Sources` collection (Lab 1)
5. Apply classifications to the following columns:

    | Column | Classification to Apply |
    |--------|------------------------|
    | `full_name` | **Person's Name** |
    | `email` | **Email Address** |
    | `ssn` | **U.S. Social Security Number (SSN)** |
    | `date_of_birth` | **Date of Birth** |
    | `phone` | **U.S. Phone Number** |
    | `address` | **U.S. Street Address** (or **Person's Address** if available) |

6. Click **Save**
7. Verify the classification tags now appear on those columns

**Step 2: Classify the Dimension Customer Table (Fabric)**

8. Search for `dimension_customer` → click the Fabric Lakehouse table
9. Click **Schema** → **Edit**
10. On the `Customer` column → add classification: **Person's Name**
11. On the `Postal Code` column → add classification: **U.S. Zip Code**
12. Click **Save**

**Step 3: Classify the Databricks Customer Table**

13. Search for `customer` → click the result from the Databricks `samples.tpch` schema
14. Click **Schema** → **Edit**
15. On the `c_name` column → add classification: **Person's Name**
16. On the `c_address` column → add classification: **Person's Address** (or **All Full Names** if Address isn't available)
17. On the `c_phone` column → add classification: **U.S. Phone Number**
18. Click **Save**

**Step 4: Cross-Platform Classification Comparison**

19. Compare the classified assets across all sources:

    | Asset | Source | Classifications Applied |
    |-------|--------|------------------------|
    | `employees` | Fabric Lakehouse | SSN, Email, Name, Phone, DOB, Address (6 columns) |
    | `dimension_customer` | Fabric Lakehouse | Person's Name, Zip Code (2 columns) |
    | `tpch.customer` | Databricks UC | Person's Name, Address, Phone (3 columns) |

20. Key takeaway: The same classification labels (Person's Name, Phone Number, etc.) apply across both Fabric and Databricks — enabling unified governance policies regardless of where the data lives. In enterprise environments, auto-classification handles ADLS/SQL sources while manual classification covers Fabric and Databricks.

**Expected Result**: Classifications applied to employee and customer tables across Fabric and Databricks. Same governance labels used consistently across platforms.

---

## Task 3: Review Technical Lineage Across Platforms (20 min)

> Lineage in Purview tracks **data movement**. When data flows from one asset to another via a pipeline or copy activity, Purview captures it as a lineage diagram. In this task, you'll create a pipeline that moves your employee data from the Lakehouse to the Warehouse, then view the lineage Purview captures.

**Step 1: Create a Data Pipeline in Fabric**

1. Go to the **Fabric portal** (`https://app.fabric.microsoft.com`)
2. Navigate to your workspace (`Purview-Lab-WS`)
3. Click **+ New item** → select **Data pipeline**
4. **Name**: `Employee-ETL-Pipeline` → click **Create**

**Step 2: Add and Configure a Copy Activity**

5. In the pipeline canvas, click **Copy data** (from the activity toolbar)
6. Click on the Copy data activity to configure it

7. **Source** tab:
   - Click **+ New** next to Connection
   - Select **Microsoft Fabric Lakehouse** → select `Purview-Lakehouse`
   - Under **Table**, browse and select: `employees`
     > This is the PII-rich employee table you uploaded in Task 1

8. **Destination** tab:
   - Click **+ New** next to Connection
   - Select **Microsoft Fabric Warehouse** → select `Purview-Warehouse`
   - Under **Table option**, select **Auto create table**
   - Enter **Table name**: `stg_employees`

**Step 3: Run the Pipeline**

9. Click **Run** → click **Save and run** if prompted
10. Wait for the pipeline to complete (1-2 minutes)
11. Verify **Status: Succeeded**

**Step 4: Verify the Data Moved**

12. Go back to the workspace → click on **Purview-Warehouse**
13. Expand **dbo** → **Tables** → you should see `stg_employees`
14. Right-click → **Select TOP 1000 rows** → verify the 10 employee records appear
    > This is the same employee data from the Lakehouse, now in the Warehouse

**Step 5: Re-Scan Fabric to Capture Lineage**

15. Switch to **Purview portal** → **Data Map** → **Data sources** → click `Purview-Fabric`
16. Click **+ New scan** (or re-run):
    - **Name**: `Scan-Fabric-Lineage`
    - **Credential**: Microsoft Purview MSI (system)
    - Scope: `Purview-Lab-WS` workspace
    - Scan rule set: System default
    - Trigger: Once
17. Click **Save and Run**
18. Wait for **Completed** status (3-5 minutes)

**Step 6: View the Lineage Diagram**

19. Go to **Data Catalog** → search for `stg_employees`
20. Click on the **stg_employees** asset (in the Warehouse)
21. Click the **Lineage** tab
22. You should see a lineage diagram:

    ```
    ┌──────────────┐     ┌───────────────────────┐     ┌──────────────┐
    │   employees   │ ──→ │ Employee-ETL-Pipeline  │ ──→ │ stg_employees │
    │  (Lakehouse)  │     │  (Data Pipeline)       │     │  (Warehouse)  │
    └──────────────┘     └───────────────────────┘     └──────────────┘
    ```

    - **Left**: `employees` — the source table you uploaded and classified
    - **Middle**: `Employee-ETL-Pipeline` — the pipeline that moved the data
    - **Right**: `stg_employees` — the destination staging table

23. Click on each node to see details — source links to the Lakehouse table, destination links to the Warehouse table

24. Go back → search for `employees` → click the Lakehouse table → **Lineage** tab
25. You should see the same lineage from the source side (arrow going OUT to the pipeline)

    > **Note**: If lineage doesn't appear immediately after the scan, wait 10-15 minutes. Purview processes lineage asynchronously.

**Step 7: Compare Lineage Across All Sources**

26. Check lineage on the **Semantic model**: search for the Power BI Dataset → **Lineage** tab
    - May show SQL analytics endpoint → Semantic model connection

27. Check lineage on a Databricks asset: search for `tpch.customer` → **Lineage** tab
    - Shows **"Not available"** — the `samples` catalog is read-only, no data was moved

28. Lineage summary across all sources:

    | Asset | Lineage Visible? | Why? |
    |-------|-----------------|------|
    | `employees` (Lakehouse) | ✅ Yes — arrow to Pipeline | Pipeline copies data FROM this table |
    | `stg_employees` (Warehouse) | ✅ Yes — arrow from Pipeline | Pipeline copies data TO this table |
    | `Employee-ETL-Pipeline` | ✅ Yes — connects source to destination | Pipeline is the data movement activity |
    | Semantic model | ✅ May show SQL endpoint → Dataset | Fabric tracks item-level connections |
    | `tpch.customer` (Databricks) | ❌ Not available | No data movement — read-only catalog |

29. Key takeaway: **Lineage requires data movement.** Purview captures it automatically when you use Fabric Pipelines, Dataflows, or Databricks notebooks that write data. No lineage appears for static/read-only data.

