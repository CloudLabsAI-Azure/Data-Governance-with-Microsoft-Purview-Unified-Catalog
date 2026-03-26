# Lab 5: Unified Search & Discovery Across Platforms

## Objective

Search and discover data assets across both Fabric and Databricks from a single Unified Catalog, compare metadata completeness between platforms, and identify ownership and documentation gaps.

## Task 1: Search Data Assets Across Fabric and Databricks (20 min)

1. Navigate back to the **Purview portal**.
2. In the left sidebar, click **Unified Catalog** > **Discovery** > **Data assets**.
   
4. Now lets serach for Data Assets dimension_customer then press **Enter**

5. Review results — you should see assets from **both** platforms:

   | Asset | Source | Type |
   |-------|--------|------|
   | `dimension_customer` | Fabric — SalesLakehouse | Lakehouse table |
   | `samples.tpch.customer` | Databricks Unity Catalog | UC table |

5. Click on the **Fabric** `dimension_customer` → review the asset detail page:
   - **Overview**: source type, workspace, collection path
   - **Schema**: columns — Customer, Category, Buying Group, Postal Code, etc.
   - **Classifications**: any classifications you applied in Lab 4 (Person's Name, Zip Code)
   - **Properties**: OneLake path, format (Delta)
6. Click **Back** → click on the **Databricks** `samples.tpch.customer` → review:
   - **Schema**: `c_custkey`, `c_name`, `c_address`, `c_phone`, `c_nationkey`, `c_acctbal`, `c_mktsegment`, `c_comment`
   - **Properties**: catalog path (`samples` → `tpch` → `customer`), workspace URL

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

**Step 4: Document Completeness Summary**

11. Based on your review, note the pattern:

    | Metadata | Fabric Lakehouse | Fabric Semantic Model | Databricks UC |
    |----------|-----------------|----------------------|---------------|
    | Schema | ✅ Auto-discovered | ✅ Auto-discovered | ✅ Auto-discovered |
    | Classifications | ✅ Manual (Lab 4) | ❌ Not scanned | ✅ Manual (Lab 4) |
    | Description | ❌ Manual needed | ❌ Manual needed | Partial (UC may have) |
    | Owner | ❌ Manual needed | ❌ Manual needed | ❌ Manual needed |
    | Glossary terms | ❌ Manual needed | ❌ Manual needed | ❌ Manual needed |

> **Key takeaway**: Scanning gives you schema and classifications automatically. Descriptions, ownership, and glossary terms require manual curation — which is what Labs 6 and 7 address.

**Expected Result**: Metadata completeness compared across Fabric Lakehouse, Fabric Semantic Model, and Databricks Unity Catalog. Common gaps identified: missing descriptions, owners, and glossary terms.

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


