# Day 2 - Lab 6: Create and Manage Data Products

## Lab Overview

In this lab, you will create and manage data products in Microsoft Purview by combining data assets from multiple platforms such as Microsoft Fabric and Azure Databricks. You will define governance domains, create a data product with business context, and associate relevant data assets to build a unified, business-ready dataset.

You will then enrich the data product with governance metadata such as ownership, descriptions, use cases, and contacts. Finally, you will publish the data product to the Unified Catalog and validate how business users can discover and explore it through search and governance domain navigation. :contentReference[oaicite:0]{index=0}

## Lab Objectives

In this lab, you will perform the following:

- **Task 1:** Create a Data Product Spanning Fabric and Databricks  
- **Task 2:** Assign Domain, Owner, and Business Description  
- **Task 3:** Publish Data Product to Unified Catalog  

## Estimated Duration 60 minutes

## Task 1: Create a Data Product Spanning Fabric and Databricks

> **What is a Data Product?** A data product is a curated, business-ready collection of data assets packaged for consumption. It groups related assets from any source (Fabric, Databricks, ADLS, etc.) into a single discoverable unit with business context, ownership, and access policies.

**Step 1: Create a Governance Domain**

1. Navigate to the **Purview portal** 

   ```
   https://purview.microsoft.com
   ```
1. From the left navigation pane, click **Solutions (1)**, then select **Unified Catalog (2)**.

   ![Picture 1](./Media/DG13.png)

1. In the **Unified Catalog** page, expand **Catalog management (1)**, select **Governance domains (2)**, and click **Create governance domain (3)**.

   ![Picture 1](./Media/DG53.png)

1. In the **New governance domain** page, enter the following details and click **Next (4)**:

      | Field        | Value                                                                |
      |--------------|----------------------------------------------------------------------|
      | Name         | Sales Analytics **(1)**                                              |
      | Description  | Governance domain for sales-related data assets across Fabric and Databricks platforms **(2)**|
      | Type     | Data domain **(3)**                                                      |

      ![Picture 1](./Media/DG54.png)

1. On the **Custom attributes** step, leave the default settings and click **Create (5)**.

   ![Picture 1](./Media/DG56.png)

1. Verify that the **Sales Analytics** governance domain appears in the list.

   ![Picture 1](./Media/DG55.png)

**Step 2: Create the Data Product**

1. Click **Unified Catalog** → **Catalog management** → **Data products**
1. Click **+ New data product**
1. On the **Basic details** step:
   - **Name**: `Customer 360`
   - **Description**: `Unified customer data product spanning Fabric Lakehouse and Databricks Unity Catalog for customer analytics and reporting.`
   - **Type**: select `Dataset`
1. Click **Next** → on **Business details**:
    - **Governance domain**: select `Sales Analytics`
    - **Description** (if available): `Customer data product that consolidates customer profiles, geographic data, and sales transactions from Fabric and Databricks for unified analytics.`
    - **Owners**: add your lab user account
1. Click **Next** → on **Custom attributes**, skip → click **Create**

**Step 3: Add Assets to the Data Product**

1. After creation, select **Add data assets** → the **Find and select** panel opens with a search box, Collection filters (Databricks Sources, Fabric Sources), and Classification filters
1. Search for and add these **core assets** (you can select multiple before clicking **Add**):
    - **Fabric assets**: `dimension_customer` (Lakehouse Table)
    - **Databricks assets**: `customer` (Azure Databricks Table), `sales_suppliers` (Azure Databricks Table)

   > **Tip**: Use the **Collection** filter to narrow results to just Fabric Sources or Databricks Sources when multiple results appear.

1. Optionally, add more assets to enrich the data product:
    - **Fabric**: `dimension_city`,`dimension_customer`, `fact_sale` (if available in your Lakehouse)
    - **Databricks**: any additional tables from your custom catalog
1. Verify the assets appear in the data product's asset list (minimum 3 assets)

   > **Note**: This data product spans two platforms (Fabric + Databricks) — demonstrating Purview's ability to package cross-platform assets into a single business unit.

   **Expected Result**: `Sales Analytics` governance domain created. `Customer 360` data product created with assets from both Fabric and Databricks (minimum 3: `dimension_customer`, `customer`, `sales_suppliers`).

## Task 2: Assign Domain, Owner, and Business Description

**Step 1: Review Data Product Metadata**

1. Open the `Customer 360` data product
1. Review the metadata already set:
   - **Name**: Customer 360
   - **Description**: cross-platform customer data product description
   - **Governance domain**: Sales Analytics
   - **Owner**: your lab user account

**Step 2: Add Additional Business Context**

1. Click **Edit** on the data product
1. Add or update:
   - **Use case**: `Customer analytics, segmentation, sales reporting, cross-platform customer matching`
   - **Update frequency**: `Fabric data refreshes daily via Lakehouse; Databricks data is static reference (TPC-H benchmark)`
   - **Quality notes**: `Fabric customer data sourced from Wide World Importers sample. Databricks customer data is TPC-H standard benchmark. Both scanned and classified by Purview.`
   
1. Click **Save**

## Task 3: Publish Data Product to Unified Catalog

**Step 1: Review Before Publishing**

1. Open the `Customer 360` data product
1. Verify all required fields are populated:
   - Name and description
   - Governance domain (`Sales Analytics`)
   - Owner assigned
   - At least one data asset added
1. Review the data product status — it should be in **Draft** state

**Step 2: Publish the Data Product**

1. Click **Publish** (or change status to **Published**)
1. Confirm the publish action
1. The data product status changes to **Published**

   > **What happens when you publish?** Published data products become visible to all users with catalog reader permissions. Business users can discover them through search, browse, and governance domain navigation. Draft products are only visible to owners and admins.

**Step 3: Verify Discovery as a Business User**

1. Go to **Unified Catalog** → **Discovery** → **Data products**
1. Verify `Customer 360` appears in the data products list
1. Click on it → confirm all metadata is visible:
   - Description, use case, governance domain
   - Owner and contacts
   - List of included assets (6 assets from Fabric + Databricks)
1. Go to **Unified Catalog** → **Discovery** → **Data assets** → search for `Customer 360`
    - The data product should appear as a searchable entity
1. Go to **Unified Catalog** → **Catalog management** → **Governance domains** → click `Sales Analytics`
    - The `Customer 360` data product should appear under this domain

**Step 4: Browse by Governance Domain**

1. Go to **Unified Catalog** → **Discovery** → **Browse**
1. Select **By governance domain** → click `Sales Analytics`
1. Verify `Customer 360` data product is listed
1. Click into it → navigate to individual assets → confirm the full drill-down path:
    - Domain → Data Product → Asset → Schema → Columns

**Step 5: Create a Second Data Product (Optional)**

1. If time permits, create a second data product:
    - **Name**: `Sales Transactions`
    - **Description**: `Sales and order transaction data across Fabric and Databricks for revenue analysis`
    - **Domain**: `Sales Analytics`
    - **Assets**: `fact_sale` (Fabric) + any available Databricks order/sales tables
    - **Publish** it
1. Verify both data products appear under the `Sales Analytics` domain

   >**Expected Result**: `Customer 360` data product published and discoverable in Unified Catalog. Business users can find it via search, data products listing, and governance domain browsing. Full drill-down from domain → product → asset → schema works.

## Summary

In this lab, you created and managed a data product in Microsoft Purview by defining a governance domain, combining data assets from Microsoft Fabric and Azure Databricks, and assigning business metadata such as owner, description, and use case. You then published the data product to the Unified Catalog and validated its discoverability and usability from a business user perspective.

## Click Next to continue to the next lab.

![](./Media/GS0001.png)