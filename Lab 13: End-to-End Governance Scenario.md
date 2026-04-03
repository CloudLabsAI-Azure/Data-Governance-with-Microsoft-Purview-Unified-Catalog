# Day 4 - Lab 13: End-to-End Governance Scenario

## Estimated Duration: 80 minutes

## Lab Overview

In this lab, you will bring together all governance capabilities learned across the 4-day workshop. You will create a derived table in Fabric using a notebook, apply full governance controls to the new asset, and perform a comprehensive end-to-end review of the entire governance framework using the Unified Catalog.

This lab demonstrates the complete governance lifecycle — from data creation and scanning through to full curation including quality monitoring, data product membership, and cross-platform discovery.

## Lab Objectives

In this lab, you will perform the following:

- **Task 1:** Create a Derived Table and Track Lineage
- **Task 2:** Validate Governance, Quality, and Security Controls
- **Task 3:** Final Review Using Unified Catalog

## Task 1: Create a Derived Table and Track Lineage

In this task, you will create a Fabric notebook that reads from existing Lakehouse tables and writes a new derived table. After re-scanning, you will review the lineage captured by Purview.

**Step 1: Create a Fabric Notebook**

1. Switch to the **Fabric portal** (`https://app.fabric.microsoft.com`)
2. Go to the `Purview-Lab-WS` workspace
3. Click **+ New item** → select **Notebook**
4. Name it: `Import-Databricks-Data`
5. Attach the notebook to **PurviewLakehouse**:
   - In the notebook toolbar, look for the Lakehouse selector
   - Select **PurviewLakehouse** as the default lakehouse

6. In the notebook, add a cell with the following PySpark code:

   ```python
  # Create a customer revenue summary from existing Lakehouse data
   df_customers = spark.sql("SELECT * FROM dimension_customer")
   df_sales = spark.sql("SELECT * FROM fact_sale")
   
   # Aggregate sales per customer
   customer_summary = df_sales.groupBy("CustomerKey").agg(
       {"TotalIncludingTax": "sum", "SaleKey": "count"}
   ).withColumnRenamed("sum(TotalIncludingTax)", "TotalRevenue") \
    .withColumnRenamed("count(SaleKey)", "OrderCount")
   
   # Join with customer dimension
   result = customer_summary.join(
       df_customers.select("CustomerKey", "Customer", "Category", "BuyingGroup"),
       on="CustomerKey",
       how="inner"
   )
   
   # Write to Lakehouse as a new table
   result.write.mode("overwrite").format("delta").saveAsTable("customer_revenue_summary")
   
   print(f"Created customer_revenue_summary with {result.count()} rows")
   ```

7. Click **Run all** → wait for execution to complete
8. Go to `PurviewLakehouse` → **Tables** → confirm `customer_revenue_summary` table exists

**Step 2: Re-Scan Fabric to Capture New Asset**

9. Switch to **Purview portal** → **Data Map** → **Data sources**
10. Click `Contoso-Fabric` → **+ New scan** (or re-run existing scan)
11. Configure same settings as Lab 2 → scope: `Purview-Lab-WS` → run scan
12. Wait for scan to complete

**Step 3: View Lineage for the New Table**

13. Go to **Unified Catalog** → **Discovery** → **Data assets**
14. Search for `customer_revenue_summary`
15. Click on the asset → go to the **Lineage** tab
16. Review the lineage graph:
    - You may see the **PurviewLakehouse** and the **Notebook** as connected items
    - Purview captures item-level lineage (Lakehouse → Notebook)
17. If lineage is visible, click on each node to review the metadata

## Task 2: Validate Governance, Quality, and Security Controls

In this task, you will apply all governance layers to the newly created table — demonstrating the full governance lifecycle from scan to complete curation.

**Step 1: Apply Full Governance to the New Asset**

1. Search for `customer_revenue_summary` in **Data assets**
2. Click **Edit** and apply all governance metadata:
   - **Description**: `Customer revenue summary table. Aggregates total revenue and order count per customer from the Wide World Importers retail dataset. Derived from dimension_customer and fact_sale via Fabric notebook.`
   - **Owner**: add your lab user account
   - **Expert**: add your lab user account
3. Click **Save**

**Step 2: Add Glossary Term**

4. Click **Edit** again → under **Glossary terms** dropdown → select `Revenue` → **Save**
5. Verify `Revenue` appears under Glossary terms on the asset

**Step 3: Add to Data Product**

6. Go to **Catalog management** → **Data products** → `Customer 360`
7. Click **+ Add assets** → search for `customer_revenue_summary` → add it
8. The data product now contains the original assets plus the new derived table

**Step 4: Create a Quality Rule**

9. Go to **Health management** → **Data quality**
10. Select the **Sales Analytics** domain → **Data assets** → add `customer_revenue_summary` if not already added
11. Navigate to the asset → **Rules** tab → **+ New rule**
12. Select **Empty/blank fields** → configure for the `Customer` column → **Create**
13. Click **Run quality scan** → wait for completion

**Step 5: Verify All Governance Layers**

14. Search for `customer_revenue_summary` → click on the asset
15. Verify the complete governance picture:

    | Governance Layer | Status |
    |-----------------|--------|
    | Schema | Auto-discovered |
    | Classifications | Auto-detected during scan |
    | Owner | Your lab account |
    | Description | Business context documented |
    | Glossary terms | Revenue |
    | Data product | Customer 360 |
    | Quality score | From quality scan |
    | Lineage | Item-level |

16. This is a fully governed asset — the complete governance lifecycle demonstrated

## Task 3: Final Review Using Unified Catalog

In this task, you will perform a comprehensive review of the entire governance framework built across the 4-day workshop, testing end-to-end discovery scenarios.

**Step 1: Walk Through the Complete Governance Hierarchy**

1. Navigate the full hierarchy top-down:
   - **Governance domain**: `Sales Analytics`
     - **Data products**: `Customer 360`, `Enterprise Master Data`
       - **Assets**: tables from Fabric + Databricks
         - Schema, Classifications, Quality scores, Glossary terms, Owners

**Step 2: Test End-to-End Discovery Scenarios**

2. **Scenario 1 — Business user looking for customer data**:
   - Search `Customer` → finds glossary term + all customer assets across platforms
   - Click `Customer 360` data product → sees all curated customer data with quality scores

3. **Scenario 2 — Compliance officer checking sensitive data**:
   - Filter by classification `Person's Name` → finds all PII-containing assets
   - Review classification details on asset schema tabs

4. **Scenario 3 — Data engineer checking quality**:
   - Go to **Health management** → **Data quality** → review all active rules and scores
   - Identify any assets below quality threshold

5. **Scenario 4 — MDM team finding golden records**:
   - Open `Enterprise Master Data` product → sees curated golden records

**Step 3: Review What Each Day Accomplished**

6. Summary of the 4-day governance journey:

   | Day | Focus | What Was Built |
   |-----|-------|---------------|
   | 1 | Foundation | Purview setup, Fabric + Databricks connections, scanning, classifications |
   | 2 | Discovery & Products | Cross-platform search, data products, glossary terms |
   | 3 | Quality & MDM | Quality rules, trust assessment, golden records |
   | 4 | Governance & Compliance | Access governance, health management, classifications, lineage, end-to-end |


### Summary

In this lab, you:

- Created a derived table in Fabric using a PySpark notebook
- Re-scanned to capture the new asset and lineage in Purview
- Applied full governance controls: description, owner, glossary, data product, quality
- Validated the complete governance lifecycle on a single asset
- Tested end-to-end discovery scenarios for different user personas
- Reviewed the 4-day governance journey from zero to comprehensive framework

### Key Governance Layers Built
1. **Data Map**: Sources registered, scanned, metadata captured
2. **Classifications**: Auto-detected PII across Fabric + Databricks
3. **Unified Catalog**: Cross-platform search and discovery
4. **Data Products**: Business-ready curated data packages
5. **Glossary**: Standard business vocabulary
6. **Data Quality**: Rules, scores, and monitoring
7. **Master Data**: Golden records identified via data products
8. **Access Governance**: Centralized visibility with platform-native enforcement
9. **Health Management**: Governance maturity controls and improvement actions
10. **Lineage**: Item-level data flow traceability
11. **Audit**: Activity logging and governance metrics via Data Estate Insights

# Congratulations! You have successfully completed Day 4.
    
