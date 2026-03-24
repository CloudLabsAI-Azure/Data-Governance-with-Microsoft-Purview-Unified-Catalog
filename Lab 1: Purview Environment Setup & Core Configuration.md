# Lab 1: Purview Environment Setup & Core Configuration 

### Objective:
Configure Microsoft Purview by validating access roles, organizing governance structure using collections and domains, and enabling the Unified Catalog experience.

### Estimated Duration: 20 minutes

### Task 1: Validate Microsoft Purview Account and Access Roles

In this task, you will verify access to the Microsoft Purview account and confirm that the required roles are assigned.

1. In the **Azure portal** home page, scroll down and select **Resource groups**.

    ![Picture 1](../Media/sandbox-purview-image1.png)

1. In the **Resource groups** pane, review the list and select **rg-purview-governance-lab**.

     ![Picture 1](../Media/sandbox-purview-image2.png)

1. Locate **purview-2146201** and click on it.

    ![Picture 1](../Media/sandbox-purview-image3.png)

1. Click **Open Microsoft Purview Governance Portal** to launch the portal in a new tab.

    ![Picture 1](../Media/sandbox-purview-image4.png)

1. When **Welcome to the new Microsoft Purview portal!** pop-up appears, click on **Get started**.

   ![Picture 1](../Media/sandbox-purview-image6.png)
   
1. On the **Microsoft Purview** portal, from the left navigation pane select **Solutions** (1) and then select **Data Map** (2).

   ![Picture 1](../Media/sandbox-purview-image7.png)

1. Under **Data Map**, select **Domains (1)**, ensure **purview (2)** is listed, and then click on **Role assignments (3)**.

   ![Picture 1](../Media/sandbox-purview-image5.png)

1. Review all the roles assigned to your user account.

   ![Picture 1](../Media/sandbox-purview-image8.png)
   
   ![Picture 1](../Media/sandbox-purview-image9.png)



1. In the Purview portal. Go to Settings (gear icon) → Roles and permissions

1. Verify your account has the following roles:

   - Purview Data Curator (edit metadata and classifications)
   
   - Purview Data Source Administrator (register and scan data sources)
   
   - Purview Data Reader (browse catalog)
   
   - Collection Admin on the root collection

1. If any role is missing. Navigate to Data Map > Collections > Root Collection

1. Select Role assignments > Add.

1. Assign the missing role to your user account

   **>Note**: Wait 2–3 minutes for role propagation


### Task 2: Configure Collections, Domains, and Ownership Model (20 min)

1. Go to **Data Map** → **Collections** in the Purview portal
2. Click on the **root collection** → **Add a sub-collection**
3. Create the following hierarchy:

   | Collection Name | Parent | Purpose |
   |----------------|--------|---------|
   | `Contoso Data Estate` | Root | Top-level org collection |
   | `Fabric Sources` | Contoso Data Estate | All Fabric assets |
   | `Databricks Sources` | Contoso Data Estate | All Databricks assets |
   | `Shared Assets` | Contoso Data Estate | Cross-platform curated assets |


5. **Configure Domains** (if Unified Catalog is active):
   - Go to **Unified Catalog** → **Domains** (or **Data Map** → **Domains**)
   - Click **+ New domain**
   - Create two domains:
     - **Name**: `Sales & Commerce` | **Description**: `All sales, orders, and customer data`
     - **Name**: `Human Resources` | **Description**: `Employee PII and HR data`
   - Assign a **Domain owner**: your user account for both

6. **Set Data Ownership** on collections:
   - Click on `Fabric Sources` collection → **Role assignments**
   - Add yourself as **Data Source Admin** and **Data Curator**
   - Repeat for `Databricks Sources` and `Shared Assets`



### Task 3: Enable Unified Catalog Experience

In this task, you will enable and explore the Unified Catalog experience.

1. Navigate to https://purview.microsoft.com

1. Check if Unified Catalog is visible in the left navigation

1. If not visible. Go to Settings → Data Governance

1. Select Activate or Start free trial

   **>Note**: Wait 5–10 minutes for activation and refresh the portal

1. Once enabled, explore:

   - Unified Catalog → Browse (view domains and collections)
   
   - Unified Catalog → Search (centralized search experience)
   
   - Unified Catalog → Glossary (currently empty)
   
   - Unified Catalog → Data Products (currently empty)

1. Verify:

   - Domains (Sales & Commerce, Human Resources) are visible

   - Collection-based browsing is available


























===============================================================
## Objective:

Set up and validate the Microsoft Purview environment by verifying access roles, organizing governance structure using collections and domains, and enabling the Unified Catalog experience.

### Estimated Duration: 20 minutes

### Task 1: Validate Microsoft Purview Account and Access Roles

In this task, you will confirm that your Microsoft Purview account is accessible and that you have the required permissions to perform governance activities.

1. Sign in to the Azure portal using the provided lab credentials.

1. Search for and open your Microsoft Purview account.

1. Launch the Microsoft Purview Governance Portal.

1. Navigate to Settings → Collections.

1. Verify that your user account is assigned appropriate roles such as:

   - Collection Admin
    
   - Data Curator
    
   - Data Reader
    
   - Ensure you have access to the root collection.


