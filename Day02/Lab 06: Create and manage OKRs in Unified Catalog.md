# Lab 06: Create and Manage OKRs in Microsoft Purview Unified Catalog

## Estimated Duration: 120 Minutes

## Lab Overview

In this lab, you will create and manage Objectives and Key Results
(OKRs) in Microsoft Purview Unified Catalog. OKRs help organizations
align data governance initiatives with measurable business outcomes.

This lab focuses on governance-driven OKRs, such as improving glossary
coverage, increasing data quality visibility, and enhancing domain-level
accountability.

This lab is fully independent and does not rely on previous labs.

## Lab Objectives

In this lab, you will perform the following:

-   **Task 1:** Verify Required Roles for OKR Management
-   **Task 2:** Access Unified Catalog and Open OKRs
-   **Task 3:** Create a Governance-Focused Objective
-   **Task 4:** Define and Configure Key Results
-   **Task 5:** Assign OKR Owners and Contributors
-   **Task 6:** Validate OKR Visibility and Governance Alignment

## Task 1: Verify Required Roles for OKR Management

In this task, you will verify that your account has permissions to
create and manage OKRs.

1.  Open a web browser and navigate to:

    https://purview.microsoft.com

2.  From the left navigation pane of the Microsoft Purview portal,
    select **Settings (1)**.

3.  Under Settings, select **Roles and access (2)**.

4.  Verify that your user account has one of the following roles:

    -   Governance Domain Owner
    -   Data Steward
    -   OKR Contributor (if available)
    -   Global Catalog Reader (for visibility)

> **Important:** Without proper governance permissions, you will not be
> able to create or manage OKRs.

### Optional Task: Assign Required Roles (If Not Visible)

If you cannot create OKRs, follow these steps.

#### Step A: Assign Purview Administrator Role in Azure

1.  Open the Azure Portal.
2.  In the Search resources, services, and docs (G+/) (1) box, enter
    **Microsoft Purview accounts (2)**.
3.  Select your Purview account (3).
4.  From the left navigation pane, select **Access control (IAM) (4)**.
5.  Click **+ Add (5)** → **Add role assignment (6)**.
6.  Select **Purview Administrator (7)**.
7.  Assign to your user account (8).
8.  Click **Review + Assign (9)**.

Wait a few minutes for propagation.

#### Step B: Assign Data Steward Role in Purview Portal

1.  Return to https://purview.microsoft.com.
2.  Select **Settings (1)** → **Roles and access (2)**.
3.  Select **Data Steward (3)**.
4.  Click **+ Add members (4)**.
5.  Select your user account (5).
6.  Click **Save (6)**.

Sign out and sign back in.

## Task 2: Access Unified Catalog and Open OKRs

In this task, you will access the OKR section within Unified Catalog.

1.  From the left navigation pane of the Microsoft Purview portal,
    select **Unified Catalog (1)**.

2.  On the Unified Catalog homepage, locate and select **OKRs (2)** from
    the governance components list.

3.  Review any existing objectives displayed on the page.

## Task 3: Create a Governance-Focused Objective

In this task, you will create a new data governance objective.

1.  On the OKRs page, click **+ New objective (1)**.

2.  On the Create objective page:

    -   Enter **Improve Data Governance Maturity (2)** as the Objective
        name.
    -   In the Description field (3), enter: "Enhance organizational
        data governance practices by increasing glossary coverage, data
        ownership, and governance visibility."

3.  Optionally assign a Governance Domain (4) if available.

4.  Set the timeframe (5), such as Quarterly.

5.  Click **Create (6)**.

## Task 4: Define and Configure Key Results

In this task, you will define measurable key results aligned with the
governance objective.

1.  Select the objective **Improve Data Governance Maturity (1)**.

2.  Click **+ Add key result (2)**.

3.  Configure the first Key Result:

    -   Title (3): Increase glossary term coverage by 30%
    -   Description (4): Expand glossary definitions to cover critical
        business concepts.
    -   Measurement type (5): Percentage
    -   Target value (6): 30

4.  Click **Save (7)**.

5.  Repeat the process to create additional governance-focused Key
    Results, such as:

    -   Achieve 100% domain ownership assignment
    -   Improve data quality visibility score by 25%
    -   Tag 80% of critical assets with glossary terms

## Task 5: Assign OKR Owners and Contributors

In this task, you will assign ownership and responsibility for the
objective.

1.  Select the objective **Improve Data Governance Maturity (1)**.

2.  Locate the **Owner (2)** field.

3.  Click **+ Assign owner (3)**.

4.  Search for and select the appropriate user account (4).

5.  Click **Save (5)**.

6.  Optionally assign contributors under the Contributors section (6).

> **Note:** Assigning ownership ensures accountability for governance
> progress.

## Task 6: Validate OKR Visibility and Governance Alignment

In this task, you will validate that the OKR is visible and properly
configured.

1.  From the OKRs page, confirm that the objective appears in the list.

2.  Select the objective to verify:

    -   Objective description is visible
    -   Key Results are listed
    -   Target metrics are configured
    -   Assigned owner is displayed

3.  Use the search bar (1) at the top of the Purview portal to search
    for the objective name and confirm discoverability.

4.  Optionally sign in as a Global Catalog Reader to verify visibility.

## Review

In this lab, you have:

-   Verified OKR-related governance roles
-   Created a governance-focused objective
-   Defined measurable key results
-   Assigned OKR ownership
-   Validated OKR visibility and configuration

You have successfully completed Lab 06: Create and Manage OKRs in
Microsoft Purview Unified Catalog.