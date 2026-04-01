# Lab 8: Data Quality Rules and Monitoring

**Duration**: 50 minutes
**Day**: 3 — Data Quality & MDM Integration Use Cases

## Objective

Define data quality rules on Fabric and Databricks assets, execute quality checks, and review quality metrics in the Unified Catalog.

> **Prerequisites**: Labs 1–7 completed. Fabric Lakehouse and Databricks Unity Catalog assets scanned, data products and glossary terms created.


## Task 1: Configure Data Quality Source Connections for Fabric and Databricks

Data quality in Microsoft Purview connects directly to the data source to execute rule queries. For Fabric Lakehouse tables, Purview uses the SQL analytics endpoint.

**For Microsoft Fabric (customer_master):**

1. In the **Fabric portal**, navigate to the workspace and open the **Lakehouse**. 

    ![Picture 1](./Media/sandbox-purview-image205.png)

1. Copy the **workspace ID** from the URL (1), as shown below, as it will be required in later steps. Then, from the same URL, copy the **Lakehouse ID (2)** that appears after `lakehouse/`.

    ![Picture 1](./Media/sandbox-purview-image207.png)

1. In the purview portal, open **Unified Catalog**, expand **Health management (1)**, select **Data quality (1)** > **Sales Analytics**. And from the top menu click on **Manage**
   
      ![Picture 1](./Media/sandbox-purview-image203.png)

1. Select **+ New** then provide the following connection details:
   - **Connection name**: **fabric-dq-connection (1)**
   - **Source Type**:Choose **Fabric (2)**
   - **Worksapce id**: paste the id you copied in the previous step(3)
   - **Lakehouse id**: paste the id you copied in the previous step(4)
   - Click **Submit (5)** after the connection is tested

     ![Picture 1](./Media/sandbox-purview-image208.png)


## Task 2: Define Data Quality Validation Rules for Dataset

1. For each rule below, navigate to **Unified Catalog** > **Health management** > **Data quality (1)** > **Customer Intelligence (2)** domain.

   ![](../media/jj9.png)

1. Click on **Customer Intelligence** and select **customer_master**

   ![](../media/jj10.png)

1. Select **Rules** and click on **New Rule**

   ![](../media/jj11.png)





















































*******************************************************************************************************************
---

## Task 1: Define Data Quality Rules on Selected Assets (20 min)

> **What is Data Quality in Purview?** Microsoft Purview Data Quality lets you define rules that validate data correctness, completeness, and consistency. Rules run against scanned assets and produce quality scores visible in the Unified Catalog.

**Step 1: Navigate to Data Quality**

1. Navigate to the **Purview portal** (`https://purview.microsoft.com`)
2. In the left sidebar, click **Unified Catalog** → **Health management** → **Data quality**
3. You should see the Data Quality overview page

**Step 2: Create Rule 1 — Empty/Blank Fields**

4. Click **+ New rule** → select **Empty/blank fields**
5. Configure:
   - **Name**: `Customer Name Completeness`
   - **Description**: `Looks for blank and empty customer name fields`
   - **Governance domain**: `Sales Analytics`
6. Click **Create** → open the rule → **Add columns**
7. Search for `dimension_customer` → select the **Customer** column → click **Add**

**Step 3: Create Rule 2 — Freshness**

8. Click **+ New rule** → select **Freshness**
9. Configure:
   - **Name**: `Sales Data Freshness`
   - **Description**: `Validates that sales data has been updated within expected timeframes`
   - **Governance domain**: `Sales Analytics`
10. Click **Create** → open the rule → **Add columns**
11. Search for `fact_sale` → select a date column → click **Add**

**Step 4: Create Rule 3 — Unique Values**

12. Click **+ New rule** → select **Unique values**
13. Configure:
    - **Name**: `Customer Key Uniqueness`
    - **Description**: `Confirms that customer key values are unique`
    - **Governance domain**: `Sales Analytics`
14. Click **Create** → open the rule → **Add columns**
15. Search for `dimension_customer` → select **Customer Key** → click **Add**

**Step 5: Create Rule 4 — String Format Match**

16. Click **+ New rule** → select **String format match**
17. Configure:
    - **Name**: `Vendor Email Format`
    - **Description**: `Validates that vendor email addresses follow expected format`
    - **Governance domain**: `Sales Analytics`
18. Click **Create** → open the rule → **Add columns**
19. Search for `vendors` → select **contact_email** → click **Add**
**Step 6: Verify Rules Created**

25. Go to **Data quality rules** → verify all 4 rules appear:

    | Rule | Type | Target Asset | Target Column |
    |------|------|-------------|---------------|
    | Customer Name Completeness | Completeness | Fabric `dimension_customer` | Customer |
    | Sales Data Freshness | Freshness | Fabric `fact_sale` | Date column |
    | Customer Key Uniqueness | Uniqueness | Databricks `tpch.customer` | `c_custkey` |
    | Phone Number Format | Format | Databricks `tpch.customer` | `c_phone` |

**Expected Result**: 4 data quality rules created covering completeness, freshness, uniqueness, and format validation across both Fabric and Databricks assets.

---

## Task 2: Execute Data Quality Checks (15 min)

**Step 1: Run Quality Scan on Fabric Assets**

1. In **Data quality**, select the `Customer Name Completeness` rule
2. Click **Run** (or **Evaluate**)
3. Wait for the quality check to complete — this samples the data and evaluates against the rule
4. Review the result:
   - **Pass rate**: percentage of rows where customer name is not null/empty
   - **Rows evaluated**: total rows sampled
   - **Failed rows**: count of rows that violated the rule
5. Repeat for `Sales Data Freshness` rule → run and review results

**Step 2: Run Quality Scan on Databricks Assets**

6. Select the `Customer Key Uniqueness` rule → click **Run**
7. Review results:
   - **Pass rate**: should be 100% (TPC-H `c_custkey` is a primary key, all values unique)
   - This confirms the benchmark data has no duplicate keys
8. Select the `Phone Number Format` rule → click **Run**
9. Review results:
   - Pass rate depends on how many phone values match the expected format
   - TPC-H phone numbers follow a `XX-XXX-XXX-XXXX` pattern

**Step 3: Review Quality Run History**

10. For each rule, click **Run history** (or **Evaluation history**)
11. Review:
    - Timestamp of each run
    - Pass/fail counts per run
    - Trend over time (currently just 1 run — in production you'd see trends)

**Step 4: Document Results**

12. Note the quality results summary:

    | Rule | Asset | Pass Rate | Notes |
    |------|-------|-----------|-------|
    | Customer Name Completeness | Fabric `dimension_customer` | Expected ~100% | Sample data is complete |
    | Sales Data Freshness | Fabric `fact_sale` | Varies | Static sample data — freshness may show as stale |
    | Customer Key Uniqueness | Databricks `tpch.customer` | Expected 100% | Primary key — no duplicates |
    | Phone Number Format | Databricks `tpch.customer` | Varies | TPC-H format `XX-XXX-XXX-XXXX` |

**Expected Result**: All 4 quality rules executed successfully. Pass rates visible for each rule. Quality evaluation history recorded.

---

## Task 3: Review Quality Metrics in Unified Catalog (15 min)

**Step 1: View Quality Scores on Assets**

1. Go to **Unified Catalog** → **Discovery** → **Data assets**
2. Search for `dimension_customer` → click on the Fabric Lakehouse version
3. Look for a **Data quality** tab or section on the asset detail page
4. Review:
   - Quality score for the asset (aggregated from all rules applied to it)
   - Individual rule results (Customer Name Completeness pass rate)
   - Quality status indicator (green/yellow/red based on thresholds)
5. Search for `samples.tpch.customer` → review quality scores:
   - Customer Key Uniqueness: 100%
   - Phone Number Format: varies

**Step 2: Quality and Data Products**

6. Go to **Unified Catalog** → **Catalog management** → **Data products** → click `Customer 360`
7. Check if quality information is visible at the data product level:
    - Assets within the data product should show their individual quality scores
    - The data product quality is an aggregate of its constituent assets
8. Note: Quality visibility on data products will be explored further in **Lab 9**

**Step 3: Set Up Quality Alerts (If Available)**

9. In **Data quality** settings, check for alert/notification options:
    - Configure alerts when quality drops below a threshold (e.g., pass rate < 95%)
    - Set notification recipients (your lab user account)
10. If alert configuration is not available in the current Purview version, note this as a feature to review in future updates

**Expected Result**: Quality scores visible on individual assets in Unified Catalog. Quality monitoring established for cross-platform assets.

---

## Lab 8 Summary

| Task | What You Did | Key Takeaway |
|------|-------------|--------------|
| 1 | Created 4 quality rules (completeness, freshness, uniqueness, format) | Quality rules validate data correctness across platforms |
| 2 | Executed quality checks on Fabric + Databricks assets | Quality evaluation produces pass rates and identifies issues |
| 3 | Reviewed quality metrics in Unified Catalog and Insights | Quality scores visible on assets and in governance dashboards |

