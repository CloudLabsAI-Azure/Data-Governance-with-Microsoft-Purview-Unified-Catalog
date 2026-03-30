# Lab 5: Unified Search & Discovery Across Platforms

**Duration**: 50 minutes
**Day**: 2  Unified Catalog, Discovery & Data Products

## Objective

Search and discover data assets across both Fabric and Databricks from a single Unified Catalog, compare metadata completeness between platforms, and identify ownership and documentation gaps.

## Task 1: Search Data Assets Across Fabric and Databricks (20 min)

1. Navigate to the **Purview portal** (`https://purview.microsoft.com`)
2. In the left sidebar, click **Unified Catalog** → **Discovery** → **Data assets**

**Step 2: Cross-Platform Keyword Search**

3. In the search bar, type `customer` → press Enter
4. Review results — you should see assets from **both** platforms in one result set. Fabric Lakehouse tables like `dimension_customer`, `fact_sale` appear alongside Databricks tables like `customer` from `samples.tpch`, `samples.tpcds_sf1`, `samples.bakehouse`, etc. The `PurviewLakehouse` Power BI Dataset also appears.

5. Click on the **Fabric** `dimension_customer` (Lakehouse Table) → review the asset detail page:
   - **Overview**: source type, workspace, collection path
   - **Schema**: columns — Customer, Category, Buying Group, Postal Code, etc.
   - **Classifications**: any classifications you applied in Lab 4 (Person's Name, Zip Code)
   - **Properties**: OneLake path, format (Delta)


**Step 3: Search by Different Criteria**

7. Search for `sale` → Fabric shows `fact_sale` (Lakehouse Table), Databricks shows `store_sales`, `sales_customers`, `sales_transactions` from various schemas
8. Search for `orders` → Databricks shows `samples.tpch.orders`. Fabric has no match (WWI uses `fact_sale` instead)
9. Search for `vendors` → verify your uploaded vendor table appears (Fabric Lakehouse)


7. Click **Back** → scroll down in the results → find the **Databricks** `customer` tables. You will see multiple `customer` tables from different schemas:
   - `samples.tpcds_sf1.customer`
   - `samples.tpcds_sf1000.customer`
   - `samples.tpch.customer`
   - `samples.wanderbricks.customer`
   - `samples.bakehouse.customer`
   > **Tip**: To identify the right one, check the **Fully qualified name** shown below each result — look for `schemas/tpch/tables/customer`. It may be further down the list.
8. Click on the `samples.tpch.customer` entry → review:
   - **Schema**: `c_custkey`, `c_name`, `c_address`, `c_phone`, `c_nationkey`, `c_acctbal`, `c_mktsegment`, `c_comment`
   - **Properties**: catalog path (`samples` → `tpch` → `customer`), workspace URL

**Step 3: Search by Different Criteria**

10. Search for `trips` → verify only Databricks `samples.nyctaxi.trips` appears

**Step 4: Use Filters to Narrow Results**

11. In the search results page, use the left filter panel:
    - **Source type**: select `Fabric` → only Fabric assets shown
    - Clear filter → select `Azure Databricks Unity Catalog` → only Databricks assets shown
    - Clear filter
12. Filter by **Classification**: select `Person's Name` → see which assets across both platforms have name-related PII (assets you classified in Lab 4)
13. Filter by **Collection**: select `Fabric Sources` or `Databricks Sources` to scope by your collection hierarchy

**Step 5: Browse by Source Type**

14. Go to **Unified Catalog** → **Discovery** → **Browse**
15. Select **By source type** → click **Fabric** → explore the workspace → artifact hierarchy
16. Go back → click **Azure Databricks Unity Catalog** → explore catalog → schema → table hierarchy
17. Note how **Browse** gives a hierarchical view while **Search** gives a flat cross-platform view

**Expected Result**: Cross-platform search returns assets from both Fabric and Databricks in a single result set. Filters allow narrowing by source type, classification, and collection. Browse provides hierarchical navigation per source.

---

## Task 2: Compare Metadata Completeness (15 min)

> **Why compare?** Different source types provide different levels of metadata. Understanding completeness gaps helps prioritize where manual curation is needed.

**Step 1: Compare Customer Assets**

1. Search for `dimension_customer` → open the **Fabric** `dimension_customer` (Lakehouse table)
2. On the asset detail page, check these metadata fields:

   | Metadata Field | Present? |
   |---------------|----------|
   | Schema (columns + types) | ✅ |
   | Classifications | ✅ (applied manually in Lab 4: Person's Name, Zip Code) |
   | Description | ❌ (empty — not auto-populated) |
   | Owner | ❌ (not assigned) |
   | Glossary terms | ❌ (none linked) |
   | Contacts (Expert / Owner) | ❌ (not set) |

3. Click **Back** → search for `customer` → find the **Databricks** `samples.tpch.customer` (check the fully qualified name to pick the correct one from the list)
4. Check the same metadata fields:

   | Metadata Field | Present? |
   |---------------|----------|
   | Schema (columns + types) | ✅ |
   | Classifications | ✅ (applied manually in Lab 4: Person's Name, Address, Phone) |
   | Description | ✅ (provided by Unity Catalog by default) |
   | Owner | ❌ (not assigned in Purview) |
   | Glossary terms | ❌ (none linked) |
   | Contacts (Expert / Owner) | ❌ (not set) |

**Step 2: Compare the Vendors Table**

5. Search for `vendors` → click on the Fabric Lakehouse version
6. Check metadata — this should be the most complete asset from Lab 4:
   - Schema: ✅ (11 columns including tax_id, contact_email, phone, address)
   - Classifications: ✅ (6 classifications applied in Lab 4: Tax ID, Email, Name, Phone, Date, Address)
   - Description: ❌
   - Owner: ❌
7. Compare with `fact_sale` (Fabric) and `samples.tpch.orders` (Databricks) — both have schema but fewer or no classifications

**Step 3: Compare Semantic Model Metadata**

8. Search for `PurviewLakehouse` → click on the **Power BI Dataset** / **Semantic model** asset
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
    | Classifications | ✅ Manual (Lab 4) | ❌ Not scanned | ✅ Manual (Lab 4) |
    | Description | ❌ Manual needed | ❌ Manual needed | ✅ From Unity Catalog |
    | Owner | ❌ Manual needed | ❌ Manual needed | ❌ Manual needed |
    | Glossary terms | ❌ Manual needed | ❌ Manual needed | ❌ Manual needed |

> **Key takeaway**: Scanning gives you schema and classifications automatically. Databricks Unity Catalog provides descriptions by default, but Fabric assets need manual descriptions. Ownership and glossary terms require manual curation on all platforms — which is what Labs 6 and 7 address.

**Expected Result**: Metadata completeness compared across Fabric Lakehouse, Fabric Semantic Model, and Databricks Unity Catalog. Common gaps identified: missing descriptions, owners, and glossary terms.

---

## Task 3: Identify Ownership and Documentation Gaps (15 min)

**Step 1: Review Current Governance Gaps**

1. Based on your Task 2 review, note that most assets have:
   - Schema: ✅ (auto-discovered by scan)
   - Classifications: ✅ only on assets you manually classified in Lab 4
   - Description: ❌ empty on all assets
   - Owner: ❌ not assigned on any asset
   - Glossary terms: ❌ none linked
2. This means the catalog has technical metadata but no business context — business users can't tell what the data means or who owns it

**Step 2: Assign Ownership to Key Assets**

3. Go to **Unified Catalog** → **Discovery** → **Data assets**
4. Search for `dimension_customer` → click on the **Fabric Lakehouse** version
5. Click **Edit** (pencil icon)
6. On the **Overview** tab:
   - **Asset description**: enter `Customer dimension table from Wide World Importers retail dataset. Contains customer names, categories, buying groups, and postal codes.`
   - **Certified**: optionally toggle to **Yes**
7. Click **Contacts** tab on the left:
   - **Experts**: search your lab user account (e.g., `ODL_User`) → add it
   - **Owners**: search your lab user account → add it
8. Click **Save**

> **Note**: Databricks assets from the `samples` catalog cannot be edited in Purview (no Edit button). This is because the `samples` catalog is a read-only built-in catalog. In a real environment with your own Databricks catalogs, you would be able to edit those assets.

**Step 3: Verify Updates**

10. Search for `dimension_customer` again → click on the asset → verify:
    - Owner now shows your account
    - Description is populated
    - These fields persist across searches and are visible to all catalog users

> **Note**: You cannot repeat this for Databricks `samples.tpch.customer` because the `samples` catalog is read-only — no Edit button is available.

**Step 4: Review Remaining Gaps**

12. Note that only 1 asset now has an owner and description (Fabric `dimension_customer`). Databricks assets from the `samples` catalog cannot be edited. The remaining assets still need curation — this will be addressed with **Data Products** (Lab 6) and **Glossary Terms** (Lab 7)

**Expected Result**: The Fabric `dimension_customer` asset now has an owner and description. Databricks `samples` catalog confirmed as read-only. Remaining governance gaps identified for Labs 6 and 7.


