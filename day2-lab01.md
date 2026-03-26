# Lab 5: Unified Search & Discovery Across Platforms

## Objective

Search and discover data assets across both Fabric and Databricks from a single Unified Catalog, compare metadata completeness between platforms, and identify ownership and documentation gaps.

## Task 1: Search Data Assets Across Fabric and Databricks (20 min)

1. Navigate back to the **Purview portal**.

3. In the left sidebar, click **Unified Catalog** > **Discovery** > **Data assets**.

     ![Picture 1](./Media/sandbox-purview-image67.png)
   
5. Now lets serach for **Data Assets** **dimension_customer** then press **Enter**.

    ![Picture 1](./Media/sandbox-purview-image68.png)
   
1. This will take you to a page where you can search and review data assets across **Fabric** and **Databricks**.
    
1. From the left navigation pane, under Filters, expand **Data source** and select either **Fabric, Databricks**, or both to review the assets.

    ![Picture 1](./Media/sandbox-purview-image69.png)
       
6. If you select both, review the results—you should see assets from both platforms:

   ![Picture 1](./Media/sandbox-purview-image70.png)

## Task 2: Compare Metadata Completeness (15 min)

> **Why compare?** Different source types provide different levels of metadata. Understanding completeness gaps helps prioritize where manual curation is needed.

**Step 1: Compare Customer Assets**

1. Seelct **Fabric** then click `dimension_customer` (Lakehouse table).

   ![Picture 1](./Media/sandbox-purview-image71.png)

3. On the asset detail page, check these metadata fields:

   | Metadata Field | Present? |
   |---------------|----------|
   | Schema (columns + types) | Yes |
   | Classifications | No |
   | Assest Description | (empty — not auto-populated) |
   | Owner |  (not assigned) |
   | Glossary terms |  (none linked) |
   | Contacts (Expert / Owner) | (not set) |

   ![Picture 1](./Media/sandbox-purview-image72.png)

4. Click **Back** and select the checkbox to filter the **Databricks** then choose **`customer`**.

    ![Picture 1](./Media/sandbox-purview-image73.png)
   
6. Check the same metadata fields:

   | Metadata Field | Present? |
   |---------------|----------|
   | Schema (columns + types) | Yes |
   | Classifications | No |
   | Assest Description | (empty — not auto-populated) |
   | Owner |  (not assigned) |
   | Glossary terms |  (none linked) |
   | Contacts (Expert / Owner) | (not set) ||

   ![Picture 1](./Media/sandbox-purview-image74.png)

## Task 3: Identify Ownership and Documentation Gaps (15 min)

6. Go to **Unified Catalog** → **Discovery** → **Data assets**
7. Search for `dimension_customer` → click on the **Fabric Lakehouse** version
8. Click **Edit** (pencil icon)
   
10. In the **Description** field, enter: `Customer dimension table from Wide World Importers retail dataset. Contains customer names, categories, buying groups, and postal codes.`
9. In the **Contacts** section:

   - **Owner**: add your lab user account
   - **Expert**: add your lab user account
   - Click **Save**

      ![Picture 1](./Media/sandbox-purview-image75.png)

      ![Picture 1](./Media/sandbox-purview-image76.png)

12. Repeat for any for Databricks:
    - **Owner**: add your lab user account
    - **Description**: Auto filled
    - Click **Save**

## Task 3:1: Verify Updates**

13. Search for `customer` again → click on each asset → verify:
    - Owner now shows your account
    - Description is populated
    - These fields persist across searches and are visible to all catalog users


