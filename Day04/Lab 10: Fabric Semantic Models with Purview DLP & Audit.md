# Day 4 - Lab 10: Fabric Semantic Models with Purview DLP & Audit

## Estimated Duration: 150 Minutes

## Lab Overview

In this lab, you will configure Microsoft Fabric together with Microsoft
Purview to understand how governance, Data Loss Prevention (DLP), and
audit monitoring work across analytics workloads.

You will:

-   Create a Microsoft Fabric workspace
-   Create a semantic model
-   Configure a Microsoft Purview DLP policy targeting Fabric / Power BI
-   Simulate a data-sharing scenario
-   Review audit logs from the Microsoft Purview portal

This lab follows a guided configuration approach and avoids impacting
production environments.

## Lab Objectives

In this lab, you will perform the following:

-   **Task 1:** Verify Required Roles and Access
-   **Task 2:** Create a Microsoft Fabric Workspace
-   **Task 3:** Create a Fabric Semantic Model
-   **Task 4:** Configure a Microsoft Purview DLP Policy
-   **Task 5:** Simulate Policy Enforcement in Fabric
-   **Task 6:** Search and Review Audit Logs in Microsoft Purview

## Task 1: Verify Required Roles and Access

In this task, you will verify that your account has the required
permissions in both Microsoft Fabric and Microsoft Purview.

### Step 1: Verify Fabric Access

1.  Open a web browser and navigate to:

    https://app.fabric.microsoft.com

2.  After signing in, from the left navigation pane of the Fabric home
    page, select **Workspaces (1)**.

3.  Confirm that you can view existing workspaces and that the **+ New
    workspace (2)** option is visible.

> If the New workspace option is not visible, you may not have
> Contributor or Admin permissions in Fabric.

### Step 2: Verify Microsoft Purview Portal Access

1.  Open a new browser tab and navigate to:

    https://purview.microsoft.com

2.  After signing in, from the left navigation pane of the Microsoft
    Purview portal, select **Solutions (1)**.

3.  From the list of available solutions, select **Data loss prevention
    (2)**.

4.  Confirm that the **Policies (3)** option is available.

5.  From the left navigation pane, again select **Solutions (4)** and
    then choose **Audit (5)**.

6.  Confirm that the **Search (6)** page loads successfully.

> Required roles typically include Compliance Administrator, Security
> Administrator, or DLP permissions.

## Task 2: Create a Microsoft Fabric Workspace

In this task, you will create a dedicated workspace for governance
testing.

1.  Return to the Microsoft Fabric portal.

2.  From the left navigation pane, select **Workspaces (1)**.

3.  Click **+ New workspace (2)** in the upper-right corner.

4.  On the Create workspace pane:

    -   Enter **Fabric Governance (3)** in the Name field.
    -   In the Description field (4), enter:
        "Workspace used for testing Purview DLP and audit integration."

5.  Review workspace settings and click **Apply (5)**.

6.  Confirm that the new workspace opens successfully.

## Task 3: Create a Fabric Semantic Model

In this task, you will create a semantic model containing structured
data.

1.  Inside the **Fabric Governance Lab (1)** workspace, click **+ New
    item (2)**.

2.  From the list of available items, select **Semantic model (3)**.

3.  Choose to upload a sample dataset (CSV or Excel file) that contains
    columns such as:

    -   CustomerID
    -   CustomerName
    -   Email
    -   Revenue

4.  Follow the data import wizard:

    -   Select file (4)
    -   Review schema preview (5)
    -   Confirm import (6)

5.  After the import completes, select **Save (7)**.

6.  Enter the name:

    **Customer Analytics Model (8)**

7.  Confirm that the semantic model appears in the workspace item list.

## Task 4: Configure a Microsoft Purview DLP Policy

In this task, you will configure a DLP policy targeting Fabric / Power
BI content.

1.  Navigate to:

    https://purview.microsoft.com

2.  From the left navigation pane, select **Solutions (1)** and then
    select **Data loss prevention (2)**.

3.  On the Data loss prevention page, select **Policies (3)**.

4.  Click **+ Create policy (4)**.

5.  On the Choose a template page:

    -   Select **Custom policy (5)**.
    -   Click **Next (6)**.

6.  On the Name your policy page:

    -   Enter **Fabric Sensitive Data Protection (7)** as the policy
        name.
    -   Click **Next (8)**.

7.  On the Locations page:

    -   Scroll through the list of locations.
    -   Ensure **Microsoft Fabric or Power BI (9)** is selected.
    -   Click **Next (10)**.

8.  On the Define policy settings page:

    -   Select **Create or customize advanced DLP rules (11)**.
    -   Click **Next (12)**.

9.  Under Rule conditions:

    -   Select **Add condition (13)**.
    -   Choose **Content contains (14)**.
    -   Select a sensitive information type such as **Email address
        (15)**.
    -   Click **Add (16)**.

10. Under Actions:

    -   Select **Restrict sharing (17)** or
    -   Select **Show policy tip (18)**.

11. Click **Next (19)**, review the summary, and then select **Submit
    (20)**.

12. Wait for confirmation that the policy has been successfully created
    and deployed.

## Task 5: Simulate Policy Enforcement in Fabric

In this task, you will simulate a governance enforcement scenario.

1.  Return to the Microsoft Fabric portal.

2.  Open **Customer Analytics Model (1)**.

3.  From the top-right corner, select **Share (2)**.

4.  Attempt to share the semantic model with an external or test user
    (3).

5.  Observe whether:

    -   A policy tip appears (4)
    -   Sharing is restricted (5)

6.  Return to the Microsoft Purview portal.

7.  From the left navigation pane, select **Solutions (6)** and then
    select **Data loss prevention (7)**.

8.  Select **Alerts (8)** and review any alerts generated by the DLP
    policy.

## Task 6: Search and Review Audit Logs in Microsoft Purview

In this task, you will review audit logs for Fabric-related activity.

1.  In the Microsoft Purview portal, select **Solutions (1)**.

2.  From the list of solutions, select **Audit (2)**.

3.  On the Audit page, select **Search (3)**.

4.  Configure search filters:

    -   Activities related to Fabric or Power BI (4)
    -   Date range (5)
    -   User account (6)

5.  Click **Search (7)**.

6.  Review the results list for activities such as:

    -   Semantic model created
    -   Item shared
    -   DLP policy matched

7.  Select an activity entry (8) to review detailed event information.

## Review

In this lab, you have:

-   Verified access to Microsoft Fabric and Microsoft Purview
-   Created a Fabric workspace
-   Created a semantic model
-   Configured a DLP policy targeting Fabric
-   Simulated policy enforcement
-   Reviewed audit logs for governance tracking

You have successfully completed Lab 10 -- Fabric Semantic Models with Purview DLP & Audit.