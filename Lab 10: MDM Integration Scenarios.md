# Day 3 - Lab 10: MDM Integration Scenarios

## Lab Overview

In this lab, you will implement master data management (MDM) governance patterns using Microsoft Purview. You will identify master data entities across Fabric and Databricks, create a Classic glossary term to tag authoritative "golden record" sources, package them into a dedicated data product, and validate that master data is discoverable through the Unified Catalog.

Microsoft Purview does not include a native MDM product. This lab demonstrates how to use Purview as the catalog layer for master data governance — identifying, tagging, and linking authoritative data sources so consumers know which datasets are the trusted golden sources.

## Lab Objectives

In this lab, you will perform the following:

- **Task 1:** Identify MDM-Managed Master Data Sources
- **Task 2:** Register Authoritative Master Data in Purview
- **Task 3:** Link Golden Records to Fabric and Databricks Assets
- **Task 4:** Validate Master Data Discoverability

## Estimated Duration: 40 minutes

## Task 1: Identify MDM-Managed Master Data Sources


In this task, you will search the Unified Catalog to build a map of where the same business entities (customer, location, product) exist across Fabric and Databricks, identifying which sources should be designated as authoritative.

1. Go to **Purview portal** > **Unified Catalog** > **Discovery** > **Data assets**.

1. Search for **dimension_customer** - this is the Fabric Lakehouse customer master data.

1. Search for **customer_transactions** - this is the Databricks customer transaction data.

1. Search for **dimension_city** - note location data.

1. Search for **sales_suppliers** - note supplier/product data.

1. You're building a mental map of where the same entity exists in multiple places.

## Task 2: Register Authoritative Master Data in Purview

In this task, you will create a Classic glossary term called "Golden Record" to tag authoritative master data sources. Classic glossary terms can be mapped directly to individual assets, making them ideal for tagging golden records at the asset level.

1. Go to **Catalog management (1)** > select **Classic types (2)** under **Management Glossary** click on **View terms (3)**.

   ![Picture 1](./Media/sandbox-purview-image321.png)

1. Click **+ New term (1)** > **Continue (2)**.

   ![Picture 1](./Media/sandbox-purview-image322.png)

1. Create term:
   - **Name**: `Golden Record`
   - **Definition**: `The authoritative, trusted source of truth for a master data entity`
   - Click **Create**.
  
     ![Picture 1](./Media/sandbox-purview-image323.png) 

### Map the glossary term

1. From the **Unified Catalog** page, expand **Discovery (1)**, select **Data assets (2)**, search for **dimension_customer (3)**, and then select the **dimension_customer asset (4)**.

   ![Picture 1](./Media/DG44.png)

1. Click **Edit**

   ![Picture 1](./Media/DG106.png)

1. Click the dropdown under **Glossary terms (1)** and select **Golden Record (2)**

   ![Picture 1](./Media/sandbox-purview-image324.png)
   
1. Verify that **Golden Record** appears under selected terms, then click **Save (2)**

   ![Picture 1](./Media/DG108.png)

1. Review that **Golden Record** is displayed under **Golden Record** in the asset overview

   ![Picture 1](./Media/sandbox-purview-image324.png)

1. Repeat the same steps for **customer_transactions**, **dimension_city** and **sales_suppliers**.

## Task 3: Link Golden Records to Fabric and Databricks Assets

In this task, you will create a dedicated `Enterprise Master Data` data product to package all golden record assets together. This provides a single entry point for consumers to find authoritative master data sources.

1. Go to **Catalog management (1)** select **Data products (2)** > Click **+ New data product (3)**.

   ![Picture 1](./Media/sandbox-purview-image326.png)
   
1. In the **Create data product** page, enter the following details:

   - **Name (1):** Enter **`Enterprise Master Data`**.
   - **Description (2):** Enter *Collection of golden record master data sources – authoritative sources for Customer, Location, and Product entities*.
   - **Type (3):** Select **Dataset**.
   - **Owner (4):** Select your assigned user
   - Click **Next (5)** to continue.

     ![Picture 1](./Media/sandbox-purview-image327.png)

1. In the **Create data product** page, provide the following details:

   - **Governance domain (1):** Select **Sales Analytics**.
   - **Use cases (2):** Enter *Master data governance – identifying and packaging authoritative golden record sources for Customer, Location, and Product entities across Fabric and Databricks*.
   - Click **Next (3)** to continue.

     ![Picture 1](./Media/sandbox-purview-image328.png)
 
1. Click **Create**.

1. Once the data product is created, on the **Data product created** page:

   - Ensure **Add data assets (1)** is selected under *Next steps*.
   - Click **Done (2)** to proceed.

     ![Picture 1](./Media/sandbox-purview-image329.png)

1. In the **Find and select** page:
   - Select **Fabric Sources (1)** under *Collection*.
   - Select the following assets:
     - `dimension_customer`
     - `dimension_city`

        ![Picture 1](./Media/sandbox-purview-image330.png)

1. In the same window:
   - Select **Databricks Sources (1)**.
   - Search for `customer_transactions`.
   - Select:
     - `customer_transactions`
     - `sales_suppliers`
     - Confirm all assets are listed in the **Selected (2)** pane.
     - Click **Add (3)**.     

        ![Picture 1](./Media/sandbox-purview-image331.png)

1. On the **Enterprise Master Data** page:
   - Verify that all selected assets are listed under **Data assets**:
     - `customer_transactions`
     - `sales_suppliers`
     - `dimension_customer`
     - `dimension_city`

        ![Picture 1](./Media/sandbox-purview-image332.png)
       
1. Click **Publish**.

   ![Picture 1](./Media/sandbox-purview-image333.png)
   
3. In the popup:
   - Select **Set up workflow (1)**.
   - Click **OK (2)**.

     ![Picture 1](./Media/sandbox-purview-image334.png)

1. In the **Directional Insights** section:
   - Set **Access time limit (1)** to **5 Days**.
   - Add **Approvers (2)** 
   - Click **Save changes (3)**.

     ![Picture 1](./Media/sandbox-purview-image335.png)
     
1. Click **Publish**.

   ![Picture 1](./Media/sandbox-purview-image336.png)

## Task 4: Validate Master Data Discoverability

In this task, you will verify that golden record assets are discoverable through search and data products, and confirm that the master data governance structure is visible in the Unified Catalog.

1. In the **Purview portal**, navigate to **Discovery (1)** > **Data assets (2)**. In the search bar, type **`Golden Record` (3)** and from the suggestions, select **Golden Record (4)** from the glossary results.

  ![Picture 1](./Media/sandbox-purview-image336.png)
  
1. Verify the 4 golden record assets appear in results.

    ![Picture 1](./Media/sandbox-purview-image337.png)

1. Navigate to **Discovery (1)** > **Data products (2)**. Under *Explore data products by governance domain*, select **Sales Analytics (3)**.

   ![Picture 1](./Media/sandbox-purview-image338.png)
   
3. From the list of data products, click **Enterprise Master Data**.

   ![Picture 1](./Media/sandbox-purview-image339.png)
   
5. Verify that all data assets are listed under **Data assets**, including:
   - `customer_transactions`
   - `sales_suppliers`
   - `dimension_customer`
   - `dimension_city`
   
6. Click on **dimension_customer** to open the asset details.

      ![Picture 1](./Media/sandbox-purview-image340.png)

8. In the asset details pane, click **View details**, and verify that the asset is associated with both data products:

    - **Customer 360**
    - **Enterprise Master Data**

      ![Picture 1](./Media/sandbox-purview-image341.png)

## You have successfully completed Day 3 labs, click next to continue to the next Day 4 labs.
