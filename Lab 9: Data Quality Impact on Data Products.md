# Lab 9: Data Quality Impact on Data Products

**Duration**: 50 minutes
**Day**: 3 — Data Quality & MDM Integration Use Cases

## Objective

Link quality results to data products, identify trusted vs non-trusted datasets based on quality scores, and communicate quality status to data consumers.

> **Prerequisites**: Lab 8 completed. Data quality rules created and executed on Fabric and Databricks assets. `Customer 360` data product published.

---

## Task 1: Link Quality Results to Data Products (20 min)

**Step 1: Review Current Data Product Quality**

1. Navigate to the **Purview portal** (`https://purview.microsoft.com`)
2. Click **Unified Catalog** → **Catalog management** → **Data products** → click `Customer 360`
3. Review the data product and its included assets:
   - `dimension_customer` (Fabric)
   - `dimension_city` (Fabric)
   - `dimension_date` (Fabric)
   - `customer` (Databricks — samples.tpch)
   - `sales_customers` (Databricks)
   - `sales_suppliers` (Databricks)
4. Click into each asset → check if the **Data quality** score from Lab 8 is visible on the asset detail page
5. Note which assets have quality scores and which do not:

   | Asset | Quality Rules Applied? | Quality Score |
   |-------|----------------------|---------------|
   | `dimension_customer` | ✅ Customer Name Completeness | Score from Lab 8 |
   | `dimension_city` | ❌ No rules yet | No score |
   | `dimension_date` | ❌ No rules yet | No score |
   | `customer` (Databricks tpch) | ✅ Uniqueness + Format | Score from Lab 8 |
   | `sales_customers` (Databricks) | ❌ No rules yet | No score |
   | `sales_suppliers` (Databricks) | ❌ No rules yet | No score |

**Step 2: Add Quality Rules to Uncovered Assets**

6. Go to **Health management** → **Data quality** → **Data quality rules**
7. Create a new rule:
   - **Name**: `City Name Completeness`
   - **Rule type**: **Completeness**
   - **Governance domain**: `Sales Analytics`
   - Add column: `dimension_city` → city name column
8. Click **Create** → **Run** the rule
9. Create another rule:
   - **Name**: `Order Key Uniqueness`
   - **Rule type**: **Uniqueness**
   - **Governance domain**: `Sales Analytics`
   - Add column: `samples.tpch.orders` → `o_orderkey`
10. Click **Create** → **Run** the rule
11. Now all 6 assets in the `Customer 360` data product have at least one quality rule

**Step 3: View Aggregated Quality on Data Product**

12. Go back to **Data products** → `Customer 360`
13. Review the data product quality:
    - Each asset now shows its quality score
    - The overall data product quality is the aggregate of all asset scores
    - Assets with 100% pass rates contribute positively; any failures lower the aggregate
14. If the data product page shows a **Health** or **Quality** tab, review the overall quality summary

**Expected Result**: All 6 assets in the `Customer 360` data product now have quality rules and scores. Data product quality is visible as an aggregate of individual asset quality.

---

## Task 2: Identify Trusted vs Non-Trusted Datasets (15 min)

> **What makes data "trusted"?** A trusted dataset has: (1) high quality scores, (2) assigned owner, (3) business description, (4) glossary terms linked, and (5) published in a data product. Non-trusted data lacks one or more of these.

**Step 1: Evaluate Trust Criteria**

1. Go to **Unified Catalog** → **Discovery** → **Data assets**
2. Search for `dimension_customer` (Fabric) → evaluate trust:

   | Trust Criterion | Status |
   |----------------|--------|
   | Quality score | ✅ From Lab 8 |
   | Owner assigned | ✅ From Lab 5 |
   | Description | ✅ From Lab 5 |
   | Glossary terms | ✅ `Customer` term from Lab 7 |
   | In a data product | ✅ `Customer 360` from Lab 6 |
   | Classifications | ✅ Auto-detected PII |
   | **Trust level** | **HIGH — Trusted** |

3. Search for `samples.tpch.customer` (Databricks) → evaluate:

   | Trust Criterion | Status |
   |----------------|--------|
   | Quality score | ✅ From Lab 8 |
   | Owner assigned | ❌ Read-only (samples catalog) |
   | Description | ✅ From Unity Catalog |
   | Glossary terms | ❌ Cannot edit (samples catalog) |
   | In a data product | ✅ `Customer 360` from Lab 6 |
   | Classifications | ✅ Auto-detected PII |
   | **Trust level** | **MEDIUM — Partially curated** |

4. Search for `dimension_date` (Fabric) → evaluate:

   | Trust Criterion | Status |
   |----------------|--------|
   | Quality score | ❌ No rules applied |
   | Owner assigned | ❌ Not set |
   | Description | ❌ Empty |
   | Glossary terms | ❌ None linked |
   | In a data product | ❌ Not in any product |
   | Classifications | May have auto-detected |
   | **Trust level** | **LOW — Non-trusted** |

**Step 2: Use Filters to Find Non-Trusted Assets**

5. In **Data assets** search, use filters:
   - Filter by **Classification**: see which assets have PII classifications
   - Filter by **Collection**: `Fabric Sources` vs `Databricks Sources`
   - These help identify which assets are curated vs uncurated
6. Review how many assets fall into each category:
   - **Fully curated** (quality + owner + description + glossary + data product): ~5-7 assets
   - **Partially curated** (some metadata): varies
   - **Uncurated** (scan data only): the majority of assets

**Step 3: Document Trust Assessment**

7. Create a summary of trust levels across your estate:

   | Trust Level | Criteria Met | Example Assets | Action Needed |
   |-------------|-------------|----------------|---------------|
   | **High** | All 5 criteria | `dimension_customer`, `tpch.customer` | None — ready for consumption |
   | **Medium** | 2-4 criteria | `fact_sale`, `tpch.orders` | Add missing glossary terms or descriptions |
   | **Low** | 0-1 criteria | `dimension_date`, most uncurated tables | Full curation needed |

8. Note: In a real organization, you would establish trust SLAs — e.g., "All assets in published data products must have quality score > 95%, assigned owner, and at least one glossary term"

**Expected Result**: Trust levels assessed for key assets based on quality, ownership, description, glossary, and data product membership. Most assets are low-trust (scan-only), while curated assets from previous labs are high-trust.

---

## Task 3: Communicate Quality Status to Consumers (15 min)

**Step 1: Data Product as Quality Communication Channel**

1. Go to **Unified Catalog** → **Discovery** → **Data products**
2. Click `Customer 360`
3. Review what a business consumer sees:
   - **Description**: explains the data product purpose
   - **Owner/Expert**: who to contact with questions
   - **Assets**: list of included tables with quality scores
   - **Governance domain**: `Sales Analytics`
   - **Glossary terms** on individual assets: business context
4. This is the primary way consumers discover and evaluate data quality — through the data product page

**Step 2: Review Health Management Actions**

5. Go to **Unified Catalog** → **Health management** → **Actions**
6. Review if any recommended actions are listed:
   - Assets missing quality rules
   - Assets missing owners
   - Quality scores below threshold
10. These actions guide the governance team on what to curate next

**Step 4: Create a Quality Summary for Stakeholders**

11. Based on your lab work, document the governance status:

    | Metric | Value |
    |--------|-------|
    | Total assets discovered | 30+ (Fabric + Databricks) |
    | Assets with quality scores | 7 (from Labs 8-9) |
    | Assets with owners | ~5 (from Labs 5-6) |
    | Assets with glossary terms | 7+ (from Lab 7) |
    | Published data products | 1 (`Customer 360`) |
    | Governance domains | 1 (`Sales Analytics`) |
    | Quality rules active | 6 |

12. Note: This is Day 3 of a 4-day workshop. By Day 4, all governance controls (access policies, sensitivity labels, lineage) will further improve the governance posture

**Step 5: Discuss Quality Communication Best Practices**

13. Review these principles:
    - **Data products are the primary consumption unit** — consumers should find data via products, not raw tables
    - **Quality scores build trust** — consumers can see quality before using data
    - **Owners are accountable** — every data product has a named owner
    - **Glossary creates shared language** — business and technical teams use same terms
    - **Governance reporting** — Health management Actions page shows what to curate next

**Expected Result**: Quality status communicated through data products (consumer-facing) and Health management (governance-facing). Quality communication strategy understood for production deployment.

---

## Lab 9 Summary

| Task | What You Did | Key Takeaway |
|------|-------------|--------------|
| 1 | Added quality rules to all data product assets | Every data product asset should have quality monitoring |
| 2 | Assessed trust levels across the estate | Trust = quality + ownership + description + glossary + data product |
| 3 | Reviewed quality communication channels | Data products for consumers, Health management for governance teams |
