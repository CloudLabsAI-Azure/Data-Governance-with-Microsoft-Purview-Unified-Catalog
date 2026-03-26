# Lab 5: Unified Search & Discovery Across Platforms

**Duration**: 50 minutes
**Day**: 2 — Unified Catalog, Discovery & Data Products

## Objective

Search and discover data assets across both Fabric and Databricks from a single Unified Catalog, compare metadata completeness between platforms, and identify ownership and documentation gaps.

> **Prerequisites**: Labs 1–4 completed. Fabric Lakehouse (`SalesLakehouse` in `Purview-Lab-WS`) and Databricks Unity Catalog (`samples` catalog) scanned and visible in Purview.

---

## Task 1: Search Data Assets Across Fabric and Databricks (20 min)

**Step 1: Open Unified Catalog Discovery**

1. Navigate to the **Purview portal** (`https://purview.microsoft.com`)
2. In the left sidebar, click **Unified Catalog** → **Discovery** → **Data assets**

**Step 2: Cross-Platform Keyword Search**

3. In the search bar, type `customer` → press Enter
4. Review results — you should see assets from **both** platforms:

   | Asset | Source | Type |
   |-------|--------|------|
   | `dimension_customer` | Fabric — SalesLakehouse | Lakehouse table |
   | `dimension_customer` | Fabric — SQL analytics endpoint | SQL view |
   | `dimension_customer` | Fabric — Semantic model | Power BI Dataset |
   | `samples.tpch.customer` | Databricks Unity Catalog | UC table |

5. Click on the **Fabric** `dimension_customer` → review the asset detail page:
   - **Overview**: source type, workspace, collection path
   - **Schema**: columns — Customer, Category, Buying Group, Postal Code, etc.
   - **Classifications**: any auto-detected PII (Person's Name, Postal Code)
   - **Properties**: OneLake path, format (Delta)
6. Click **Back** → click on the **Databricks** `samples.tpch.customer` → review:
   - **Schema**: `c_custkey`, `c_name`, `c_address`, `c_phone`, `c_nationkey`, `c_acctbal`, `c_mktsegment`, `c_comment`
   - **Properties**: catalog path (`samples` → `tpch` → `customer`), workspace URL

**Step 3: Search by Different Criteria**

7. Search for `sale` → review results:
   - Fabric: `fact_sale` (Lakehouse table, SQL view, semantic model)
   - Databricks: no direct match (TPC-H uses `orders`/`lineitem` not `sale`)
8. Search for `orders` → review results:
   - Fabric: `fact_order` (Lakehouse)
   - Databricks: `samples.tpch.orders` (UC table)
9. Search for `trips` → verify only Databricks `samples.nyctaxi.trips` appears

**Step 4: Use Filters to Narrow Results**

10. In the search results page, use the left filter panel:
    - **Source type**: select `Fabric` → only Fabric assets shown
    - Clear filter → select `Azure Databricks Unity Catalog` → only Databricks assets shown
    - Clear filter
11. Filter by **Classification**: select `Person's Name` → see which assets across both platforms have name-related PII detected
12. Filter by **Collection**: select `Fabric Sources` or `Databricks Sources` to scope by your collection hierarchy

**Step 5: Browse by Source Type**

13. Go to **Unified Catalog** → **Discovery** → **Browse**
14. Select **By source type** → click **Fabric** → explore the workspace → artifact hierarchy
15. Go back → click **Azure Databricks Unity Catalog** → explore catalog → schema → table hierarchy
16. Note how **Browse** gives a hierarchical view while **Search** gives a flat cross-platform view

**Expected Result**: Cross-platform search returns assets from both Fabric and Databricks in a single result set. Filters allow narrowing by source type, classification, and collection. Browse provides hierarchical navigation per source.

---

## Task 2: Compare Metadata Completeness (15 min)

> **Why compare?** Different source types provide different levels of metadata. Understanding completeness gaps helps prioritize where manual curation is needed.

**Step 1: Compare Customer Assets**

1. Search for `customer` → open the **Fabric** `dimension_customer` (Lakehouse table)
2. On the asset detail page, check these metadata fields:

   | Metadata Field | Present? |
   |---------------|----------|
   | Schema (columns + types) | ✅ |
   | Classifications | ✅ (if detected during scan) |
   | Description | ❌ (empty — not auto-populated) |
   | Owner | ❌ (not assigned) |
   | Glossary terms | ❌ (none linked) |
   | Contacts (Expert / Owner) | ❌ (not set) |

3. Click **Back** → open the **Databricks** `samples.tpch.customer`
4. Check the same metadata fields:

   | Metadata Field | Present? |
   |---------------|----------|
   | Schema (columns + types) | ✅ |
   | Classifications | ✅ (if detected during scan) |
   | Description | ✅ or ❌ (may have UC-provided description) |
   | Owner | ❌ (not assigned in Purview) |
   | Glossary terms | ❌ (none linked) |
   | Contacts (Expert / Owner) | ❌ (not set) |

**Step 2: Compare Fact Table Assets**

5. Search for `fact_sale` (Fabric) → check metadata completeness
6. Search for `samples.tpch.orders` (Databricks) → check metadata completeness
7. Note: TPC-H tables in Databricks `samples` catalog may have built-in descriptions from Unity Catalog, while Fabric Lakehouse tables from sample data typically have no descriptions

**Step 3: Compare Semantic Model Metadata**

8. Search for `SalesLakehouse` → click on the **Power BI Dataset** / **Semantic model** asset
9. Check metadata:
   - Schema shows tables + columns with BI-friendly data types
   - Relationships between dimension and fact tables may be visible
   - Description and owner are typically empty
10. Note: Semantic models have richer structural metadata (relationships, measures) but still lack business descriptions

**Step 4: Document Completeness Summary**

11. Based on your review, note the pattern:

    | Metadata | Fabric Lakehouse | Fabric Semantic Model | Databricks UC |
    |----------|-----------------|----------------------|---------------|
    | Schema | ✅ Auto-discovered | ✅ Auto-discovered | ✅ Auto-discovered |
    | Classifications | ✅ Auto-applied | ❌ Not scanned | ✅ Auto-applied |
    | Description | ❌ Manual needed | ❌ Manual needed | Partial (UC may have) |
    | Owner | ❌ Manual needed | ❌ Manual needed | ❌ Manual needed |
    | Glossary terms | ❌ Manual needed | ❌ Manual needed | ❌ Manual needed |

> **Key takeaway**: Scanning gives you schema and classifications automatically. Descriptions, ownership, and glossary terms require manual curation — which is what Labs 6 and 7 address.

**Expected Result**: Metadata completeness compared across Fabric Lakehouse, Fabric Semantic Model, and Databricks Unity Catalog. Common gaps identified: missing descriptions, owners, and glossary terms.

---

## Task 3: Identify Ownership and Documentation Gaps (15 min)

**Step 1: Check Data Estate Insights**

1. In the left sidebar, click **Data Estate Insights**
2. Click **Assets** → review:
   - **Total assets** discovered
   - **Assets with classifications** vs **without classifications**
   - **Assets with owners** vs **without owners**
3. Note the percentage of assets missing owners — this should be close to 100% since no owners have been assigned yet

**Step 2: Review Stewardship Coverage**

4. In Data Estate Insights, look for stewardship or governance metrics:
   - **Assets with description**: likely 0% or very low
   - **Assets with glossary terms**: 0%
   - **Assets with contacts/owners**: 0%
5. These gaps are the starting point for Day 2 curation work

**Step 3: Assign Ownership to Key Assets**

6. Go to **Unified Catalog** → **Discovery** → **Data assets**
7. Search for `dimension_customer` → click on the **Fabric Lakehouse** version
8. Click **Edit** (pencil icon)
9. In the **Contacts** section:
   - **Owner**: add your lab user account
   - **Expert**: add your lab user account
10. In the **Description** field, enter: `Customer dimension table from Wide World Importers retail dataset. Contains customer names, categories, buying groups, and postal codes.`
11. Click **Save**
12. Repeat for `samples.tpch.customer` (Databricks):
    - **Owner**: add your lab user account
    - **Description**: `TPC-H benchmark customer table. Contains customer key, name, address, phone, nation, account balance, and market segment.`
    - Click **Save**

**Step 4: Verify Updates**

13. Search for `customer` again → click on each asset → verify:
    - Owner now shows your account
    - Description is populated
    - These fields persist across searches and are visible to all catalog users

**Step 5: Review Remaining Gaps**

14. Go back to **Data Estate Insights** → **Assets** → note:
    - Owner coverage improved slightly (2 assets now have owners)
    - Description coverage improved slightly
    - The vast majority of assets still need curation → this will be addressed with **Data Products** (Lab 6) and **Glossary Terms** (Lab 7)

**Expected Result**: Data Estate Insights shows governance gaps (missing owners, descriptions, glossary terms). Two key customer assets now have owners and descriptions assigned. Remaining gaps identified for Labs 6 and 7.

---

## Lab 5 Summary

| Task | What You Did | Key Takeaway |
|------|-------------|--------------|
| 1 | Searched across Fabric + Databricks | Unified Catalog provides single search across all registered sources |
| 2 | Compared metadata completeness | Scanning provides schema + classifications; descriptions, owners, glossary terms need manual curation |
| 3 | Identified and started fixing gaps | Data Estate Insights tracks governance coverage; ownership and descriptions assigned to key assets |
