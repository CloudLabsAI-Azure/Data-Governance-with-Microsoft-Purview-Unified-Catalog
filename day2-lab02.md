# Lab 6: Create and Manage Data Products

**Duration**: 50 minutes
**Day**: 2 — Unified Catalog, Discovery & Data Products

## Objective

Create a data product that spans both Fabric and Databricks assets, assign governance metadata (domain, owner, description), and publish it to the Unified Catalog for business user discovery.

> **Prerequisites**: Labs 1–5 completed. Both Fabric and Databricks assets scanned and discoverable in Unified Catalog.

---

## Task 1: Create a Data Product Spanning Fabric and Databricks (20 min)

> **What is a Data Product?** A data product is a curated, business-ready collection of data assets packaged for consumption. It groups related assets from any source (Fabric, Databricks, ADLS, etc.) into a single discoverable unit with business context, ownership, and access policies.

**Step 1: Create a Governance Domain**

1. Navigate to the **Purview portal** (`https://purview.microsoft.com`)
2. Click **Unified Catalog** → **Catalog management** → **Governance domains**
3. Click **+ New governance domain**
4. Configure:
   - **Name**: `Sales Analytics`
   - **Description**: `Governance domain for sales-related data assets across Fabric and Databricks platforms`
   - **Domain owners**: add your lab user account
5. Click **Create**
6. Verify the `Sales Analytics` domain appears in the list

**Step 2: Create the Data Product**

7. Click **Unified Catalog** → **Catalog management** → **Data products**
8. Click **+ New data product**
9. Configure:
   - **Name**: `Customer 360`
   - **Description**: `Cross-platform customer data product combining Fabric retail customer dimension data with Databricks TPC-H benchmark customer data. Provides a unified view of customer information for analytics and reporting.`
   - **Governance domain**: select `Sales Analytics`
   - **Owners**: add your lab user account
10. Click **Create**

**Step 3: Add Assets to the Data Product**

11. Open the `Customer 360` data product
12. Click **+ Add assets** (or **Data assets** tab → **Add**)
13. Search for and add these assets:

    | Asset | Source | Why Include |
    |-------|--------|-------------|
    | `dimension_customer` | Fabric Lakehouse | Core customer dimension from retail dataset |
    | `dimension_city` | Fabric Lakehouse | Geographic context for customers |
    | `fact_sale` | Fabric Lakehouse | Sales transactions linked to customers |
    | `samples.tpch.customer` | Databricks UC | Benchmark customer data for cross-platform analysis |
    | `samples.tpch.orders` | Databricks UC | Order data linked to customers |

14. For each asset, search by name → select it → click **Add**
15. After adding all 5 assets, verify they appear in the data product's asset list

> **Note**: This data product spans two platforms (Fabric + Databricks) — demonstrating Purview's ability to package cross-platform assets into a single business unit.

**Expected Result**: `Sales Analytics` governance domain created. `Customer 360` data product created with 5 assets from both Fabric and Databricks.

---

## Task 2: Assign Domain, Owner, and Business Description (15 min)

**Step 1: Review Data Product Metadata**

1. Open the `Customer 360` data product
2. Review the metadata already set:
   - **Name**: Customer 360
   - **Description**: cross-platform customer data product description
   - **Governance domain**: Sales Analytics
   - **Owner**: your lab user account

**Step 2: Add Additional Business Context**

3. Click **Edit** on the data product
4. Add or update:
   - **Use case**: `Customer analytics, segmentation, sales reporting, cross-platform customer matching`
   - **Update frequency**: `Fabric data refreshes daily via Lakehouse; Databricks data is static reference (TPC-H benchmark)`
   - **Quality notes**: `Fabric customer data sourced from Wide World Importers sample. Databricks customer data is TPC-H standard benchmark. Both scanned and classified by Purview.`
5. Click **Save**

**Step 3: Add Contacts**

6. In the data product, go to the **Contacts** or **People** section
7. Add:
   - **Owner**: your lab user account (if not already set)
   - **Expert**: your lab user account
   - **Steward**: your lab user account
8. These roles determine who business users contact for questions about this data product

**Step 4: Review Asset-Level Metadata**

9. Click into each asset within the data product:
   - Verify the asset still shows its individual schema, classifications, and properties
   - Note that the asset now also shows it belongs to the `Customer 360` data product
10. The data product provides a **business layer** on top of the technical assets — business users find the data product, then drill into individual assets

**Expected Result**: Data product has complete business metadata: description, use case, governance domain, owner, expert, and steward assigned. All assets accessible from within the data product.

---

## Task 3: Publish Data Product to Unified Catalog (15 min)

**Step 1: Review Before Publishing**

1. Open the `Customer 360` data product
2. Verify all required fields are populated:
   - ✅ Name and description
   - ✅ Governance domain (`Sales Analytics`)
   - ✅ Owner assigned
   - ✅ At least one data asset added
3. Review the data product status — it should be in **Draft** state

**Step 2: Publish the Data Product**

4. Click **Publish** (or change status to **Published**)
5. Confirm the publish action
6. The data product status changes to **Published**

> **What happens when you publish?** Published data products become visible to all users with catalog reader permissions. Business users can discover them through search, browse, and governance domain navigation. Draft products are only visible to owners and admins.

**Step 3: Verify Discovery as a Business User**

7. Go to **Unified Catalog** → **Discovery** → **Data products**
8. Verify `Customer 360` appears in the data products list
9. Click on it → confirm all metadata is visible:
   - Description, use case, governance domain
   - Owner and contacts
   - List of included assets (5 assets from Fabric + Databricks)
10. Go to **Unified Catalog** → **Discovery** → **Data assets** → search for `Customer 360`
    - The data product should appear as a searchable entity
11. Go to **Unified Catalog** → **Catalog management** → **Governance domains** → click `Sales Analytics`
    - The `Customer 360` data product should appear under this domain

**Step 4: Browse by Governance Domain**

12. Go to **Unified Catalog** → **Discovery** → **Browse**
13. Select **By governance domain** → click `Sales Analytics`
14. Verify `Customer 360` data product is listed
15. Click into it → navigate to individual assets → confirm the full drill-down path:
    - Domain → Data Product → Asset → Schema → Columns

**Step 5: Create a Second Data Product (Optional)**

16. If time permits, create a second data product:
    - **Name**: `Sales Transactions`
    - **Description**: `Sales and order transaction data across Fabric and Databricks for revenue analysis`
    - **Domain**: `Sales Analytics`
    - **Assets**: `fact_sale`, `fact_order`, `fact_purchase` (Fabric) + `samples.tpch.lineitem` (Databricks)
    - **Publish** it
17. Verify both data products appear under the `Sales Analytics` domain

**Expected Result**: `Customer 360` data product published and discoverable in Unified Catalog. Business users can find it via search, data products listing, and governance domain browsing. Full drill-down from domain → product → asset → schema works.

---

## Lab 6 Summary

| Task | What You Did | Key Takeaway |
|------|-------------|--------------|
| 1 | Created governance domain + data product with cross-platform assets | Data products package assets from multiple sources into business-ready units |
| 2 | Assigned domain, owner, description, and contacts | Business metadata makes data products discoverable and accountable |
| 3 | Published and verified discoverability | Published data products are searchable by all catalog users via multiple navigation paths |
