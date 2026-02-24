# Lab 02: Create and Apply a Custom Classification in Microsoft Purview

## Estimated Duration: 120 Minutes

## Lab Overview

In this lab, you will create and apply a custom classification rule in
Microsoft Purview Data Map. You will modify the existing Azure SQL data
source (configured in Lab 01) to include a custom business identifier
pattern, create a regex-based classification rule, configure a scan rule
set, execute a new scan, and validate that the classification is
successfully applied in Unified Catalog.

This lab strictly focuses on creating and applying custom
classification.

## Lab Objectives

In this lab, you will perform the following:

-   **Task 1:** Modify Source Data to Include Custom Pattern
-   **Task 2:** Create a Custom Classification Rule
-   **Task 3:** Create a Custom Scan Rule Set
-   **Task 4:** Configure and Execute a Scan with the Custom Rule Set
-   **Task 5:** Validate Custom Classification in Unified Catalog

## Task 1: Modify Source Data to Include Custom Pattern

In this task, you will modify the existing Customers table (created in
Lab 01) to include a custom Employee ID pattern in the format EMP-XXXX
(Example: EMP-1001). This pattern will be detected using a custom regex
rule.

1.  On the **Azure Portal** page, in the **Search resources, services
    and docs (G+/) (1)** box at the top of the portal, enter **SQL
    databases (2)**, and then select **SQL databases (3)** under
    services.

2.  From the list of databases, select **PurviewLabDB (4)**.

3.  From the left navigation pane of the database blade, select **Query
    editor (Preview) (5)** and sign in using your SQL credentials.

4.  In the query editor window, paste the following SQL script:

``` sql
ALTER TABLE Customers
ADD EmployeeID NVARCHAR(20);

UPDATE Customers
SET EmployeeID = 'EMP-1001'
WHERE CustomerID = 1;

UPDATE Customers
SET EmployeeID = 'EMP-1002'
WHERE CustomerID = 2;
```

5.  Click **Run (6)** to execute the script.

    > **Important:** The EmployeeID column is required so that the
    > custom classification rule can detect a business-specific
    > identifier.

## Task 2: Create a Custom Classification Rule

In this task, you will create a regex-based classification rule to
detect Employee IDs in the format EMP-XXXX.

1.  Open a browser and navigate to **https://purview.microsoft.com**.

2.  From the left navigation pane of the Microsoft Purview portal,
    select **Data Map (1)**.

3.  Under Data Map, select **Classification rules (2)**.

4.  On the Classification rules page, click **+ New (3)**.

5.  On the Create classification rule page:

    -   In the **Name (4)** field, enter **Custom Employee ID Pattern**.
    -   In the **Description (5)** field, enter a description explaining
        that this rule detects Employee IDs in the format EMP-XXXX.
    -   Under **Rule type (6)**, select **Regex**.

6.  In the **Pattern (7)** field, enter the following expression:

```{=html}
<!-- -->
```
    EMP-d{4}

7.  Under **Data types (8)**, select **String**.

8.  Click **Create (9)**.

    > **Note:** Custom classification rules allow organizations to detect internal identifiers that are not available in built-in classification rules.

## Task 3: Create a Custom Scan Rule Set

In this task, you will create a scan rule set that includes the custom
classification rule.

1.  From the left navigation pane of the Microsoft Purview portal,
    select **Data Map (1)**.

2.  Select **Scan rule sets (2)**.

3.  Click **+ New (3)**.

4.  On the Create scan rule set page:

    -   In the **Name (4)** field, enter
        **SQL-Custom-EmployeeID-RuleSet**.
    -   Under **Data source type (5)**, select **Azure SQL Database**.

5.  Under **System classification rules (6)**, leave the default
    selections enabled.

6.  Under **Custom classification rules (7)**, locate and select
    **Custom Employee ID Pattern (8)**.

7.  Click **Create (9)**.

    > **Important:** A scan rule set determines which classification rules are applied during scanning.

## Task 4: Configure and Execute a Scan with the Custom Rule Set

In this task, you will configure and run a new full scan using the
custom scan rule set.

1.  From the left navigation pane, select **Data Map (1)** and then
    select **Sources (2)**.

2.  Select **PROD-SQL-PurviewLab (3)**.

3.  On the source overview page, click **New Scan (4)**.

4.  In the **Scan name (5)** field, enter
    **PROD-SQL-Custom-EmployeeID**.

5.  Under **Authentication method (6)**, select **Managed Identity**.

6.  Under **Scan rule set (7)**, select **SQL-Custom-EmployeeID-RuleSet
    (8)**.

7.  Under **Scan type (9)**, select **Full scan**.

8.  Click **Test connection (10)**.

9.  After successful validation, click **Run (11)**.

    > **Important:** A new scan must be executed for the custom classification rule to be applied to existing assets.

## Task 5: Validate Custom Classification in Unified Catalog

In this task, you will verify that the EmployeeID column has been
automatically classified.

1.  From the left navigation pane of the Microsoft Purview portal,
    select **Unified Catalog (1)**.

2.  In the search bar at the top of the page (2), type **Customers** and
    press Enter.

3.  From the search results, select the **Customers table (3)**.

4.  Select the **Schema tab (4)**.

5.  Locate the **EmployeeID column (5)**.

6.  Confirm that the classification **Custom Employee ID Pattern (6)**
    appears under the classification section.

    > **Note:** If the classification does not appear immediately, wait for the scan to complete and refresh the page.

## Review

In this lab, you have:

-   Modified source data to include a custom pattern
-   Created a regex-based custom classification rule
-   Created a custom scan rule set
-   Executed a new scan
-   Validated custom classification in Unified Catalog

You have successfully completed Lab 02: Create and Apply a Custom
Classification in Microsoft Purview.