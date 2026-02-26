# Day 1 - Lab 01: Register and Scan Data Sources using Microsoft Purview Data Map

## Estimated Duration: 150 Minutes

## Lab Overview

In this lab, you will configure Microsoft Purview and
perform end-to-end registration and scanning of an Azure SQL Database
using Microsoft Purview Data Map. You will provision the Purview
account, configure permissions, prepare a structured data source,
register it, execute a scan, and validate metadata in Unified Catalog.

## Lab Objectives

In this lab, you will perform the following:

- **Task 1:** Create and Configure Microsoft Purview Account  
- **Task 2:** Assign Roles and Enable Managed Identity  
- **Task 3:** Create and Prepare Azure SQL Database  
- **Task 4:** Create Sample Tables and Insert Data  
- **Task 5:** Grant Microsoft Purview Access to SQL Database  
- **Task 6:** Register Azure SQL Database in Microsoft Purview Data Map  
- **Task 7:** Configure and Execute a Scan  
- **Task 8:** Validate Metadata in Unified Catalog  

## Task 1: Create and Configure Microsoft Purview Account

In this task, you will create a Microsoft Purview account in Azure. This
account is required before accessing the Data Map and Unified Catalog
experiences in the Microsoft Purview portal.

1.  On the **Azure Portal** page, in the **Search resources, services
    and docs (G+/) (1)** box at the top of the portal, enter **Microsoft
    Purview accounts (2)**, and then select **Microsoft Purview accounts
    (3)** under services.

    ![Picture 1](../Images/purview-search.png)

2.  On the Microsoft Purview accounts page, click **+ Create (4)**.

3.  On the **Basics** tab:

    -   Select your **Subscription (5)**.
    -   Select an existing **Resource Group (6)**.
    -   In the **Account name** field, enter purview-<inject key="DeploymentID" enableCopy="false"/> **(7)**
    -   Select the default **Region (8)**.

4.  Click **Review + Create (9)** 

5. And once the validation passes select **Create (10)**.

    > **Note:** Deployment may take several minutes to complete.

6.  After deployment is completed, open the newly created **Microsoft
    Purview account (11)**.

## Task 2: Assign Roles and Enable Managed Identity

In this task, you will assign the required Purview role to your user
account and enable the system-assigned managed identity so that
Microsoft Purview can securely scan data sources.

1.  From the left navigation pane of the Purview resource blade, select
    **Access control (IAM) (1)**.

2.  At the top of the page, click **+ Add (2)** and then select **Add
    role assignment (3)**.

3.  In the Role tab, search for and select **Purview Data Curator (4)**,
    and then click **Next (5)**.

4.  On the Members tab, click **Select members (6)**, search for your
    user account (7), select it, and click **Select (8)**.

5.  Click **Review + Assign (9)** to complete the role assignment.

6.  From the left navigation pane, select **Identity (10)**.

7.  Under the System assigned tab, ensure the **Status toggle (11)**    is set to **On**, and then click **Save (12)** if required.

    > **Important:** Managed Identity is required for secure
    > authentication when scanning Azure SQL Database.


## Task 3: Create Azure SQL Database (Data Source Preparation)

In this task, you will create an Azure SQL Database that will be
registered and scanned in Microsoft Purview.

1.  Navigate back to **Azure Portal** page, in the search box at the top, enter **SQL databases (1)** and select **Azure SQL databases (2)** under services.

    ![Picture 1](../Images/sql-search.png)

2.  Click **+ Create (3)**.

3.  On the Basics tab:

    -   Select your **Subscription (4)**.
    -   Select your **Resource Group (5)**.
    -   In the **Database name (6)** field, enter **PurviewLabDB**.
    -   Under Server, click **Create new (7)** and provide required
        server details.

4.  Select **Basic pricing tier (8)**.

5.  Click **Review + Create (9)**, and then select **Create (10)**.

6.  After deployment completes, open the created **SQL Server (11)**.

7.  From the left navigation pane, select **Networking (12)**, enable
    **Allow Azure services and resources to access this server (13)**,
    and then click **Save (14)**.


## Task 4: Create Sample Tables and Insert Data

In this task, you will create a sample table and insert data to ensure
Microsoft Purview has metadata available to discover during scanning.

1.  Open the **PurviewLabDB database (1)**.

2.  From the left navigation pane, select **Query editor (Preview) (2)**
    and sign in using the SQL credentials.

3.  In the query editor window, paste the following SQL script:

``` sql
CREATE TABLE Customers (
    CustomerID INT PRIMARY KEY,
    FullName NVARCHAR(100),
    Email NVARCHAR(100),
    PhoneNumber NVARCHAR(20),
    SSN NVARCHAR(20)
);

INSERT INTO Customers VALUES
(1, 'John Doe', 'john@email.com', '9876543210', '123-45-6789'),
(2, 'Jane Smith', 'jane@email.com', '9876543222', '987-65-4321');
```

4.  Click **Run (3)** to execute the script.

    > **Note:** Columns such as Email and SSN help demonstrate automatic
    > classification during scanning.


## Task 5: Grant Microsoft Purview Access to SQL Database

In this task, you will grant the Microsoft Purview managed identity
access to the SQL database so that it can perform metadata scanning.

1.  Open the **PurviewLabDB database (1)**.

2.  From the left navigation pane, select **Access control (IAM) (2)**.

3.  Click **+ Add (3)** and select **Add role assignment (4)**.

4.  Select the **Reader role (5)**.

5.  Under Assign access to, select **Managed identity (6)**.

6.  Select the **Microsoft Purview managed identity (7)**.

7.  Click **Review + Assign (8)**.

## Task 6: Register Azure SQL Database in Microsoft Purview Data Map

In this task, you will register the Azure SQL Database as a data source
inside Microsoft Purview Data Map.

1.  Open a browser and navigate to **https://purview.microsoft.com**.

2.  From the left navigation pane of the Microsoft Purview portal,
    select **Data Map (1)**.

3.  Under Data Map, select **Sources (2)**.

4.  On the Sources page, click **+ Register (3)**.

5.  From the list of available source types, select **Azure SQL Database
    (4)** and click **Continue (5)**.

6.  On the registration page:

    -   Enter **PROD-SQL-PurviewLab (6)** as the source name.
    -   Select the appropriate **Subscription (7)**.
    -   Select the **SQL Server (8)**.
    -   Select the **Database (9)**.

7.  Click **Register (10)**.

    ![Picture 1](../Images/register-sql.png)


## Task 7: Configure and Run a Scan

In this task, you will configure a full scan using Managed Identity
authentication and execute the scan to ingest metadata into Microsoft
Purview.

1.  From the **Sources** page, select the registered source
    **PROD-SQL-PurviewLab (1)**.

2.  On the source overview page, click **New Scan (2)**.

3.  In the **Scan name (3)** field, enter **PROD-SQL-Weekly-0200**.

4.  Under **Authentication method (4)**, select **Managed Identity**.

5.  Under **Scan type (5)**, select **Full scan**.

6.  Configure the **Schedule (6)** to run during off-peak hours.

7.  Click **Test connection (7)** to validate connectivity.

8.  After successful validation, click **Run (8)**.

    > **Important:** The first scan is a full scan. Subsequent scans can
    > be configured as incremental scans.


## Task 8: Validate Metadata in Unified Catalog

In this task, you will confirm that metadata from the SQL database has
been successfully ingested into Microsoft Purview Unified Catalog.

1.  From the left navigation pane of the Microsoft Purview portal,
    select **Unified Catalog (1)**.

2.  In the search bar at the top of the page (2), type **Customers** and
    press Enter.

3.  From the search results, select the **Customers table (3)**.

4.  Review the **Overview, Schema, Columns, Classification, and Lineage
    tabs (4)** to verify metadata has been captured.


## Review

In this lab, you have:

-   Created and configured Microsoft Purview\
-   Assigned required roles and enabled Managed Identity\
-   Created Azure SQL Database and sample data\
-   Registered the data source in Data Map\
-   Configured and executed a scan\
-   Validated metadata in Unified Catalog

You have successfully completed Lab 01: Register and Scan Data Sources
using Microsoft Purview Data Map.