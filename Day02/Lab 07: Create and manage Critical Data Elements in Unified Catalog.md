# Day 02 - Lab 07: Create and Manage Critical Data Elements in Microsoft Purview Unified Catalog

## Estimated Duration: 120 Minutes

## Lab Overview

In this lab, you will create and manage Critical Data Elements (CDEs) in
Microsoft Purview Unified Catalog. Critical Data Elements represent
high-value data fields that require enhanced governance, ownership,
monitoring, and standardization across the organization.

## Lab Objectives

In this lab, you will perform the following:

-   **Task 1:** Verify Required Roles for Critical Data Element
    Management
-   **Task 2:** Access Unified Catalog and Locate Critical Data
    Elements
-   **Task 3:** Create a New Critical Data Element
-   **Task 4:** Link an Existing Glossary Term
-   **Task 5:** Publish and Validate the Critical Data Element

## Task 1: Verify Required Roles for Critical Data Element Management

In this task, you will confirm that your account has the necessary
governance permissions required to create and manage Critical Data
Elements.

1.  Open a web browser and navigate to:

    https://purview.microsoft.com

2.  After signing in, from the left navigation pane of the Microsoft
    Purview portal, scroll through the available options and select
    **Settings (1)** to access configuration and governance controls.

3.  Under the Settings section, select **Roles and access (2)**.

4.  On the Roles and access page, review the list of assigned roles and
    confirm that your user account has one of the following:

    -   **Data Steward**
    -   **Governance Domain Owner**
    -   **Global Catalog Reader** (for visibility)

> **Important:** Without Data Steward or Domain-level permissions, the
> option to create or publish Critical Data Elements will not be
> available.

## Task 2: Access Unified Catalog and Locate Critical Data Elements

In this task, you will navigate to the Critical Data Elements section
within Unified Catalog.

1.  From the left navigation pane of the Microsoft Purview portal,
    select **Unified Catalog (1)** to open the centralized governance
    experience.

2.  On the Unified Catalog homepage, locate and select **Critical data
    elements (2)** under governance components.

3.  Review any existing Critical Data Elements displayed on the page.

## Task 3: Create a New Critical Data Element

In this task, you will create a new Critical Data Element under the
Governance Domain created in Lab 04.

1.  On the **Critical data elements (1)** page, click **+ New critical
    data element (2)**.

2.  On the Create critical data element page:

    -   In the **Name (3)** field, enter: **Customer Identifier**
    -   In the **Description (4)** field, enter: "A high-value data
        element used to uniquely identify customers across systems."
    -   Under **Governance domain (5)**, select the domain created in
        Lab 04 (for example, Finance Domain).

3.  Click **Create (6)**.

The Critical Data Element will initially be created in Draft state.

## Task 4: Link an Existing Glossary Term

In this task, you will link the Critical Data Element to a Glossary term
created in Lab 05 to ensure business alignment.

1.  From the Critical data elements page, select **Customer Identifier
    (1)**.

2.  On the details page, locate the **Glossary terms section (2)**.

3.  Click **+ Add term (3)**.

4.  In the search box, enter the glossary term created in Lab 05 (for
    example, **Customer ID**) (4).

5.  Select the glossary term and click **Save (5)**.

> **Note:** Linking Critical Data Elements to Glossary terms ensures
> standardized business definitions across governance artifacts.

## Task 5: Publish and Validate the Critical Data Element

In this task, you will publish and validate the configuration of the
Critical Data Element.

1.  While viewing the **Customer Identifier (1)** Critical Data Element,
    review all configuration details, including Governance Domain and
    linked Glossary term.

2.  Click **Publish (2)** to activate the Critical Data Element.

3.  Confirm that the status changes from **Draft** to **Published**.

4.  Use the search bar (3) at the top of the Microsoft Purview portal
    and search for **Customer Identifier** to validate discoverability.

5.  Confirm that:

    -   The Governance Domain is displayed.
    -   The linked Glossary term is visible.
    -   The status shows **Published**.

## Review

In this lab, you have:

-   Verified governance permissions
-   Created a Critical Data Element within an existing Governance
    Domain
-   Linked the CDE to a Glossary term
-   Published and validated the Critical Data Element

You have successfully completed Lab 07: Create and Manage Critical Data
Elements in Microsoft Purview Unified Catalog.