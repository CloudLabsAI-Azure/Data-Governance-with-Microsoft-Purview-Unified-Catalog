# Lab 10: MDM Integration Scenarios

**Duration**: 60 minutes
**Day**: 3 — Data Quality & MDM Integration Use Cases

## Objective

Identify master data sources across the estate, register them as authoritative in Purview, link golden records to Fabric and Databricks assets, and validate that master data is discoverable through the Unified Catalog.

> **Prerequisites**: Labs 1–9 completed. Quality rules applied, data products published, glossary terms created.
>
> **Important**: Microsoft Purview does not include a native MDM product. This lab demonstrates how to **use Purview as the catalog layer for master data governance** — identifying, tagging, and linking authoritative data sources so consumers know which datasets are the trusted "golden" sources.

---

## Task 1: Identify MDM-Managed Master Data Sources (15 min)

> **What is Master Data?** Master data is the core business entities (customers, products, locations, employees) that are shared across multiple systems. In a multi-platform environment (Fabric + Databricks), the same entity may exist in multiple places — MDM governance ensures one source is designated as the "golden record."

**Step 1: Map Customer Master Data Across Platforms**

1. Navigate to the **Purview portal** (`https://purview.microsoft.com`)
2. Go to **Unified Catalog** → **Discovery** → **Data assets**
3. Search for `customer` → review all customer-related assets:

   | Asset | Platform | Role |
   |-------|----------|------|
   | `dimension_customer` | Fabric Lakehouse | Retail customer data (Wide World Importers) |
   | `dimension_customer` | Fabric SQL endpoint | SQL view of same data |
   | `dimension_customer` | Fabric Semantic model | BI layer of same data |
   | `samples.tpch.customer` | Databricks UC | Benchmark customer data (TPC-H) |

4. Note: Both platforms have customer data but with **different schemas and sources**
5. For this lab scenario, designate `dimension_customer` (Fabric Lakehouse) as the **authoritative source** — it has retail business context, is actively maintained, and feeds the BI layer

**Step 2: Map Sales Master Data**

6. Search for `fact_sale` → review:
   - `fact_sale` (Fabric Lakehouse) — retail sales transactions
   - `samples.tpch.orders` (Databricks) — benchmark order data
   - `samples.tpch.lineitem` (Databricks) — benchmark line item data
7. Note: Sales data exists in both platforms with different schemas
8. Designate `fact_sale` (Fabric) as authoritative for sales transactions

**Step 3: Document Master Data Map**

9. Summarize the master data landscape:

    | Master Entity | Authoritative Source | Platform | Secondary Sources | Platform |
    |--------------|---------------------|----------|-------------------|----------|
    | Customer | `dimension_customer` | Fabric | `samples.tpch.customer` | Databricks |
    | Location | `dimension_city` | Fabric | `samples.tpch.nation`, `region` | Databricks |
    | Sales | `fact_sale` | Fabric | `samples.tpch.orders` | Databricks |

**Expected Result**: Master data entities identified across Fabric and Databricks. Authoritative sources designated for Customer, Location, and Sales entities.

---

## Task 2: Register Authoritative Master Data in Purview (15 min)

> **How to mark authoritative sources?** Purview doesn't have a built-in "golden record" flag. We use a combination of: (1) glossary terms to tag master data, (2) descriptions to document authoritative status, and (3) a dedicated data product to package golden records.

**Step 1: Create Master Data Glossary Terms**

1. Go to **Unified Catalog** → **Discovery** → **Enterprise glossary**
2. Click **+ New term**:
   - **Name**: `Golden Record`
   - **Definition**: `The authoritative, trusted source of truth for a master data entity. When multiple systems contain the same entity, the golden record is the designated primary source. All other instances should reference or sync from this source.`
   - **Governance domain**: `Sales Analytics`
   - **Status**: `Approved`
3. Click **Create**
4. Create another term — **+ New term**:
   - **Name**: `Master Data`
   - **Definition**: `Core business entities (customers, products, locations, employees) that are shared across multiple systems and platforms. Master data requires consistent definitions, quality monitoring, and designated authoritative sources.`
   - **Governance domain**: `Sales Analytics`
   - **Status**: `Approved`
5. Click **Create**

**Step 2: Tag Authoritative Assets**

6. Go to **Data assets** → search for `dimension_customer` (Fabric Lakehouse)
7. Click **Edit** → in **Glossary terms**, add:
   - `Golden Record`
   - `Master Data`
   - `Customer` (already linked from Lab 7)
8. Update the **Description** to include: `AUTHORITATIVE SOURCE — Golden record for customer master data. This is the designated primary source for all customer information across the enterprise. Secondary sources (e.g., Databricks tpch.customer) should reference this dataset.`
9. Click **Save**

10. Repeat for `dimension_city`:
    - Add glossary terms: `Golden Record`, `Master Data`
    - Update description: `AUTHORITATIVE SOURCE — Golden record for location master data at city level.`
    - **Save**

11. Repeat for `fact_sale`:
    - Add glossary terms: `Golden Record`, `Master Data`
    - Update description: `AUTHORITATIVE SOURCE — Golden record for retail sales transactions.`
    - **Save**

**Step 3: Tag Secondary Sources**

12. Note: Databricks `samples` catalog assets are **read-only** in Purview — you cannot edit their descriptions or glossary terms. In a real environment with your own Databricks catalogs, you would tag secondary sources with `Master Data` (but NOT `Golden Record`) and add a description pointing to the authoritative source.

**Expected Result**: 3 authoritative (golden) Fabric assets tagged with `Golden Record` and `Master Data` glossary terms. Databricks secondary sources noted as read-only.

---

## Task 3: Link Golden Records to Fabric and Databricks Assets (15 min)

**Step 1: Create a Master Data Product**

1. Go to **Unified Catalog** → **Catalog management** → **Data products**
2. Click **+ New data product**
3. Configure:
   - **Name**: `Enterprise Master Data`
   - **Description**: `Collection of all golden record (authoritative) master data sources across the enterprise. Contains the designated primary sources for Customer, Location, and Product entities.`
   - **Governance domain**: `Sales Analytics`
   - **Owners**: add your lab user account
4. Click **Create**

**Step 2: Add Golden Record Assets**

5. Open `Enterprise Master Data` → click **+ Add assets**
6. Add these authoritative assets:
   - `dimension_customer` (Fabric Lakehouse) — Customer golden record
   - `dimension_city` (Fabric Lakehouse) — Location golden record
   - `fact_sale` (Fabric Lakehouse) — Sales golden record
7. Click **Add** for each

**Step 3: Publish the Master Data Product**

8. Review all fields are populated:
   - ✅ Name, description, governance domain
   - ✅ Owner assigned
   - ✅ 3 golden record assets added
9. Click **Publish**
10. The `Enterprise Master Data` data product is now discoverable by all catalog users

**Step 4: Cross-Reference with Customer 360**

11. Note that `dimension_customer` now belongs to **two** data products:
    - `Customer 360` — cross-platform analytics product (from Lab 6)
    - `Enterprise Master Data` — golden records product (this lab)
12. This is valid — an asset can belong to multiple data products serving different purposes
13. Go to `dimension_customer` asset page → verify both data products are shown in its metadata

**Expected Result**: `Enterprise Master Data` data product created and published with 3 golden record assets. Assets show membership in multiple data products.

---

## Task 4: Validate Master Data Discoverability (15 min)

**Step 1: Search by Golden Record**

1. Go to **Unified Catalog** → **Discovery** → **Data assets**
2. Search for `Golden Record` → review results
3. All 3 authoritative assets should appear (tagged with the `Golden Record` glossary term):
   - `dimension_customer` (Fabric)
   - `dimension_city` (Fabric)
   - `fact_sale` (Fabric)
4. A business user searching for "golden record" instantly finds all authoritative master data

**Step 2: Search by Master Data**

5. Search for `Master Data` → review results
6. All master data assets should appear:
   - Golden: `dimension_customer`, `dimension_city`, `fact_sale` (Fabric)
7. The `Golden Record` tag distinguishes authoritative from secondary sources

**Step 3: Navigate from Data Product**

8. Go to **Discovery** → **Data products** → click `Enterprise Master Data`
9. Verify all 3 golden records are listed
10. Click into `dimension_customer` → verify:
    - Tagged as `Golden Record` + `Master Data` + `Customer`
    - Description states "AUTHORITATIVE SOURCE"
    - Quality scores visible (from Lab 8)
    - Owner and expert assigned
11. This is the complete governance picture for a master data asset

**Step 4: Review Master Data Governance Summary**

12. Go to **Enterprise glossary** → click `Golden Record` term
13. Review linked assets — all 3 golden records should be listed
14. Go to **Catalog management** → **Governance domains** → `Sales Analytics`
15. Review the domain now contains:
    - **Data products**: `Customer 360`, `Enterprise Master Data`
    - **Glossary terms**: `Customer`, `Revenue`, `Order`, `PII`, `Golden Record`, `Master Data`
16. The governance domain is the single entry point for all sales-related data governance

**Expected Result**: Golden records discoverable via search, glossary terms, and data products. Complete MDM governance picture visible through the Unified Catalog.

---

## Day 3 Summary

| Lab | Topic | Duration | Key Outcome |
|-----|-------|----------|-------------|
| 8 | Data Quality Rules & Monitoring | 50 min | 4 quality rules created, executed, quality scores visible |
| 9 | Quality Impact on Data Products | 50 min | Quality linked to products, trust levels assessed |
| 10 | MDM Integration Scenarios | 60 min | Golden records identified, tagged, published as master data product |
| | **Total** | **160 min (~2.7 hrs)** | |

### What Was Accomplished
- Data quality rules covering completeness, freshness, uniqueness, and format across both platforms
- Trust assessment framework: quality + ownership + description + glossary + data product
- Master data governance using glossary terms (`Golden Record`, `Master Data`) to distinguish authoritative from secondary sources
- `Enterprise Master Data` product published with 3 golden records
- Secondary sources reference authoritative sources in their descriptions
