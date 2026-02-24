# Lab 01: Register and Scan Data Sources using Microsoft Purview Data Map

## Estimated Duration: 120--150 Minutes

## Lab Overview

In this lab, you will configure Microsoft Purview from scratch and
perform end-to-end data source registration and scanning using the
Microsoft Purview Data Map.

This lab focuses primarily on the Microsoft Purview portal. However,
since access to the Data Map requires a deployed Microsoft Purview
account, you will first provision the Purview account from Azure Portal
before performing governance activities inside the Purview portal.

By the end of this lab, you will:

-   Provision a Microsoft Purview account
-   Configure access control and managed identity
-   Register Azure SQL Database
-   Configure and execute a scan
-   Validate metadata discovery inside Unified Catalog

## Lab Objectives

In this lab, you will perform the following:

-   **Task 1:** Create a Microsoft Purview Account
-   **Task 2:** Configure Access Control and Managed Identity
-   **Task 3:** Access the Microsoft Purview Portal
-   **Task 4:** Register Azure SQL Database in Data Map
-   **Task 5:** Configure and Execute a Scan
-   **Task 6:** Validate Metadata Discovery in Unified Catalog

# Task 1: Create a Microsoft Purview Account

In this task, you will create a Microsoft Purview account, which is
required before accessing the Data Map and Unified Catalog.

1.  Open a web browser and navigate to the Azure Portal by entering
    https://portal.azure.com in the address bar.

2.  After signing in, locate the search bar at the top of the Azure
    Portal page labeled **Search resources, services, and docs (1)**.

3.  In the search bar, type **Microsoft Purview accounts (2)** and
    select it from the search results under Services.

4.  On the Microsoft Purview accounts page, click the **+ Create (3)**
    button to begin provisioning a new Purview account.

5.  On the Basics tab:

    -   Select your Subscription (4).
    -   Select an existing Resource Group (5).
    -   In the Account name field (6), enter a globally unique name.
    -   Choose a supported Region (7).

6.  Click **Review + Create (8)** at the bottom of the page.

7.  After validation completes successfully, click **Create (9)** to
    deploy the Purview account.

8.  Wait for the deployment process to complete. This may take several
    minutes.

### Validation

-   Deployment status shows **Succeeded**.
-   The newly created Purview account is visible in Azure Portal.

# Task 2: Configure Access Control and Managed Identity

In this task, you will assign required roles and enable the
system-assigned managed identity, which is necessary for scanning data
sources.

## Assign Required Role

1.  From the Azure Portal, open the newly created **Microsoft Purview
    account (1)**.

2.  From the left navigation pane of the Purview resource blade, select
    **Access control (IAM) (2)**.

3.  At the top of the IAM page, click **+ Add (3)** and then select
    **Add role assignment (4)**.

4.  On the Role tab, search for and select **Purview Data Curator (5)**
    (or Purview Administrator if required), and then click **Next (6)**.

5.  On the Members tab, select **Select members (7)**.

6.  Search for your user account (8), select it, and click **Select
    (9)**.

7.  Click **Review + Assign (10)** to complete the role assignment.

## Enable System Assigned Managed Identity

1.  Still within the Purview account blade, scroll in the left
    navigation pane and select **Identity (11)**.

2.  Under the System assigned tab, ensure the Status toggle (12) is set
    to **On**.

3.  If it is Off, switch it to On and click **Save (13)**.

### Validation

-   Your user account appears under Role assignments.
-   System assigned managed identity status shows as Enabled.

# Task 3: Access the Microsoft Purview Portal

In this task, you will access the Microsoft Purview governance portal to
use Data Map and Unified Catalog.

1.  Open a new browser tab and navigate to
    https://purview.microsoft.com.

2.  Sign in using the same account that was assigned the Purview role.

3.  After the portal loads, observe the left navigation pane.

4.  From the left navigation pane, select **Data Map (1)** to open the
    Data Map experience.

5.  Review the available sections such as:

    -   Sources
    -   Collections
    -   Scan rules

### Validation

-   Microsoft Purview portal loads successfully.
-   Data Map navigation is accessible without permission errors.

# Task 4: Register Azure SQL Database in Data Map

In this task, you will register an Azure SQL Database as a data source
within Microsoft Purview.

1.  From the left navigation pane of the Microsoft Purview portal, click
    **Data Map (1)**.

2.  Within Data Map, select **Sources (2)** to open the list of
    registered sources.

3.  Click the **+ Register (3)** button at the top of the Sources page.

4.  In the Register sources page, search for and select **Azure SQL
    Database (4)** from the list of available data sources.

5.  On the registration page:

    -   In the Name field (5), enter `Lab-SQL-Source`.
    -   Select the appropriate Subscription (6).
    -   Select the SQL Server (7).
    -   Select the Database (8).

6.  Click **Register (9)** to complete the source registration.

### Validation

-   The Azure SQL source appears in the Sources list.
-   The status column displays **Registered**.

# Task 5: Configure and Execute a Scan

In this task, you will configure and run a scan against the registered
SQL data source.

1.  From the Sources page in Data Map, click on **Lab-SQL-Source (1)**
    to open the source details.

2.  On the source overview page, click **New Scan (2)**.

3.  On the Scan configuration page:

    -   Under Authentication method (3), select **Managed Identity**.
    -   Under Scan type (4), select **Full scan**.
    -   Under Collection (5), select the appropriate collection.

4.  Click **Test connection (6)** to verify connectivity.

5.  After successful validation, click **Run (7)** to start the scan.

6.  Wait for the scan to complete. You may refresh the page to check
    scan status.

### Validation

-   Scan status shows **Succeeded**.
-   The number of discovered assets is greater than zero.

# Task 6: Validate Metadata Discovery in Unified Catalog

In this task, you will validate that metadata has been successfully
ingested into Unified Catalog.

1.  From the left navigation pane of the Microsoft Purview portal,
    select **Unified Catalog (1)**.

2.  In the search bar at the top of the page (2), type part of the
    database name or table name.

3.  Press Enter to display search results.

4.  Click on one of the discovered tables (3) to open the asset details
    page.

5.  Review the following sections:

    -   Overview
    -   Schema
    -   Columns
    -   Classification
    -   Lineage

6.  Click the **Lineage tab (4)** to verify that the lineage view loads
    successfully.

## Final Validation Checklist

-   Azure SQL source registered successfully
-   Scan completed without errors
-   Tables visible in Unified Catalog
-   Schema and metadata displayed
-   Lineage tab accessible

# Review

In this lab, you have:

-   Created and configured a Microsoft Purview account
-   Assigned required IAM roles
-   Enabled Managed Identity
-   Registered Azure SQL Database in Data Map
-   Executed a full scan
-   Validated metadata discovery in Unified Catalog

The Microsoft Purview governance environment is now fully operational
and ready for classification, governance domains, data quality
configuration, and advanced integrations.