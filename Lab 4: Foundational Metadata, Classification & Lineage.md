# Day 1 - Lab 4: Classification, Lineage & Cross-Platform Governance


## Overview

In Labs 2 and 3, you connected Fabric and Databricks to Purview and discovered schemas and tables. But you may have noticed:
- **No classifications** appeared on any columns
- **No lineage** (data flow diagrams) appeared on any assets

In this lab you will apply classifications to the vendor and customer data you set up in Lab 2, review the data lineage captured by the pipeline, and compare governance features across Fabric and Databricks.

## Task 1: Verify Scans and Assets (10 min)

> Before working with classifications and lineage, confirm that the scans from Labs 2 and 3 completed successfully and that all assets — including the `vendors` table you uploaded in Lab 2 — are discoverable in the catalog.

**Step 1: Verify Scan Status**

1. Navigate back to the **Purview portal**, then select **Data Map** → **Monitoring**.

2. Verify that you see two scans: one for **Fabric** and another for **Databricks**. Ensure both scans have executed successfully. The Fabric scan should show the status **Completed with exceptions**, and the Databricks scan should show the status **Completed**.

    ![Picture 1](./Media/sandbox-purview-image157.png)

## Task 2: Apply Built-in Classifications (20 min)

> Purview does **not** auto-classify data during Fabric or Databricks scans. Auto-classification (data sampling with ML/regex rules) only works for sources like Azure SQL, ADLS, and Blob Storage. For Fabric and Databricks, governance teams apply classifications **manually** — this is standard practice in enterprise environments.

**Step 1: Classify the Vendors Table (Fabric)**

1. In the **Data Catalog**, search for `vendors`
2. Click on the **vendors** Lakehouse table (source: Microsoft Fabric)
3. Click the **Schema** tab — note that **no classifications** appear (expected for Fabric)
4. Click the **Edit** button (pencil icon) at the top of the schema section
   > If you don't see Edit, verify you have **Data Curator** role on the `Fabric Sources` collection (Lab 1)
5. Apply classifications to the following columns:

    | Column | Classification to Apply |
    |--------|------------------------|
    | `full_name` | **All Full Names** |
    | `email` | **Email Address** |
    | `ssn` | **U.S. Social Security Number (SSN)** |
    | `date_of_birth` | **Date of Birth** |

        > **Note**: Columns like `employee_id`, `department`, and `salary` do not need classifications — they are not PII. Focus classifications on columns that contain personally identifiable information.

7. Click **Save**.

   ![Picture 1](./Media/sandbox-purview-image160.png)
   
9. Verify the classification tags now appear on those columns.

    ![Picture 1](./Media/sandbox-purview-image161.png)


## Task 3: Review Technical Lineage Across Platforms (20 min)

> Lineage in Purview tracks **data movement**. When data flows from one asset to another via a pipeline or copy activity, Purview captures it as a lineage diagram. In Lab 2, you created and ran a pipeline that moved vendor data from the Lakehouse to the Warehouse. Now you'll view the lineage Purview captured.

**Step 1: View the Lineage Diagram**

1. Go to **Data Catalog** → search for `stg_vendors`
2. Click on the **stg_vendors** asset (in the Warehouse)
3. Click the **Lineage** tab
4. You should see a lineage diagram:

    ```
    ┌──────────────┐     ┌───────────────────────┐     ┌──────────────┐
    │    vendors    │ ──→ │  Vendor-ETL-Pipeline   │ ──→ │  stg_vendors  │
    │  (Lakehouse)  │     │  (Data Pipeline)       │     │  (Warehouse)  │
    └──────────────┘     └───────────────────────┘     └──────────────┘
    ```

    - **Left**: `vendors` — the source table you uploaded and classified
    - **Middle**: `Vendor-ETL-Pipeline` — the pipeline you created in Lab 2
    - **Right**: `stg_vendors` — the destination staging table

5. Click on each node to see details — source links to the Lakehouse table, destination links to the Warehouse table

6. Go back → search for `vendors` → click the Lakehouse table → **Lineage** tab
7. You should see the same lineage from the source side (arrow going OUT to the pipeline)

    > **Note**: If lineage doesn't appear immediately, re-scan your Fabric source and wait 10-15 minutes. Purview processes lineage asynchronously.

**Step 2: Compare Lineage Across All Sources**

8. Check lineage on the **Semantic model**: search for the Power BI Dataset → **Lineage** tab
    - May show SQL analytics endpoint → Semantic model connection

9. Check lineage on a Databricks asset: search for `tpch.customer` → **Lineage** tab
    - Shows **"Not available"** — the `samples` catalog is read-only, no data was moved

10. Lineage summary across all sources:

    | Asset | Lineage Visible? | Why? |
    |-------|-----------------|------|
    | `vendors` (Lakehouse) | ✅ Yes — arrow to Pipeline | Pipeline copies data FROM this table |
    | `stg_vendors` (Warehouse) | ✅ Yes — arrow from Pipeline | Pipeline copies data TO this table |
    | `Vendor-ETL-Pipeline` | ✅ Yes — connects source to destination | Pipeline is the data movement activity |
    | Semantic model | ✅ May show SQL endpoint → Dataset | Fabric tracks item-level connections |
    | `tpch.customer` (Databricks) | ❌ Not available | No data movement — read-only catalog |

11. Key takeaway: **Lineage requires data movement.** Purview captures it automatically when you use Fabric Pipelines, Dataflows, or Databricks notebooks that write data. No lineage appears for static/read-only data.

**Expected Result**: Lineage diagram visible showing vendors (Lakehouse) → Vendor-ETL-Pipeline → stg_vendors (Warehouse). Databricks shows no lineage (read-only).

---

**All three Purview core capabilities demonstrated with your own data:**
- **Discovery**: Vendor data uploaded to Fabric in Lab 2, discovered alongside existing assets from Fabric and Databricks
- **Classification**: Applied to vendors table + customer tables across both platforms
- **Lineage**: Vendor data flow from Lakehouse → Pipeline → Warehouse tracked and visualized

**Next**: Day 2 — Unified Catalog, Discovery & Data Products
