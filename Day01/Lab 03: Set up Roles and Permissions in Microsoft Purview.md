# Day 1 - Lab 03: Set up Roles and Permissions in Microsoft Purview

## Estimated Duration: 90 Minutes

## Lab Overview

In this lab, you will configure governance roles and permissions in
Microsoft Purview. You will assign Data Map roles, Collection-level
roles, and Unified Catalog roles to users to control access to data
sources, classifications, and governance assets.

This lab focuses strictly on configuring and validating role-based
access control (RBAC) in Microsoft Purview.

## Lab Objectives

In this lab, you will perform the following:

-   **Task 1:** Assign Microsoft Purview Data Map Roles
-   **Task 2:** Configure Collection-Level Role Assignments
-   **Task 3:** Assign Unified Catalog Roles
-   **Task 4:** Validate Role-Based Access Control

## Task 1: Assign Microsoft Purview Data Map Roles

In this task, you will assign Data Map level roles to a user to allow
them to manage data sources and classifications.

1.  Open a browser and navigate to **https://purview.microsoft.com**.

2.  From the left navigation pane of the Microsoft Purview portal,
    select **Settings (1)**.

3.  Under the Settings section, select **Roles and access (2)**.

4.  On the Roles and access page, select the **Data Map roles (3)** tab.

5.  Select the role **Data Curator (4)**.

6.  Click **+ Add members (5)**.

7.  In the Add members pane, search for the user account (6) you want to
    assign the role to.

8.  Select the user and click **Save (7)**.

    > **Note:** The Data Curator role allows users to manage
    > classifications, glossary terms, and metadata.

## Task 2: Configure Collection-Level Role Assignments

In this task, you will assign permissions at the collection level to
control access to specific data sources.

1.  From the left navigation pane, select **Data Map (1)**.

2.  Under Data Map, select **Collections (2)**.

3.  On the Collections page, select the root collection or a specific
    collection such as **PROD-SQL-PurviewLab Collection (3)**.

4.  On the collection overview page, select **Roles (4)**.

5.  Click **+ Add role assignment (5)**.

6.  Select the role **Collection Admin (6)**.

7.  Search and select the user account (7).

8.  Click **Save (8)**.

    > **Important:** Collection-level permissions allow granular control
    > over which users can manage specific data sources.

## Task 3: Assign Unified Catalog Roles

In this task, you will assign Unified Catalog roles to allow users to
manage glossary terms, data products, and governance assets.

1.  From the left navigation pane, select **Settings (1)**.

2.  Under Settings, select **Roles and access (2)**.

3.  Select the **Unified Catalog roles (3)** tab.

4.  Select the role **Data Reader (4)** or **Data Steward (5)**
    depending on the required access level.

5.  Click **+ Add members (6)**.

6.  Search for and select the user account (7).

7.  Click **Save (8)**.

    > **Note:** Unified Catalog roles control access to governance
    > artifacts such as glossary terms and data products.

## Task 4: Validate Role-Based Access Control

In this task, you will validate that role-based access control is
functioning correctly.

1.  Sign out of the Microsoft Purview portal.

2.  Sign back in using the user account that was assigned the roles.

3.  From the left navigation pane:

    -   Verify access to **Data Map (1)** if Data Map role was assigned.
    -   Verify access to **Collections (2)** and confirm permissions
        align with assigned role.
    -   Verify access to **Unified Catalog (3)** if Unified Catalog role
        was assigned.

4.  Attempt to perform an action permitted by the assigned role (for
    example, editing metadata if assigned as Data Curator).

    > **Important:** If access is not reflected immediately, allow a few
    > minutes for role assignments to propagate.

## Review

In this lab, you have:

-   Assigned Data Map roles
-   Configured collection-level permissions
-   Assigned Unified Catalog roles
-   Validated role-based access control

You have successfully completed Lab 03: Set up Roles and Permissions in
Microsoft Purview.