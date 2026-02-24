# Day 02 -Lab 08: Create, manage and search Data Products and Assets in Unified Catalog

## Estimated Duration: 120 Minutes

## Lab Overview

In this lab, you will create, manage, and search Data Products in
Microsoft Purview Unified Catalog. Data Products represent curated,
governed, and discoverable collections of data assets that serve a
defined business purpose.

## Lab Objectives

In this lab, you will perform the following:

-   **Task 1:** Verify Required Roles for Data Product Management
-   **Task 2:** Access Unified Catalog and Locate Data Products
-   **Task 3:** Create a New Data Product
-   **Task 4:** Add Assets to the Data Product
-   **Task 5:** Configure Business Metadata and Ownership
-   **Task 6:** Publish and Search the Data Product

## Task 1: Verify Required Roles for Data Product Management

In this task, you will verify that your account has permissions required
to create and manage Data Products.

1.  Open a web browser and navigate to:

    https://purview.microsoft.com

2.  From the left navigation pane of the Microsoft Purview portal,
    select **Settings (1)**.

3.  Under the Settings section, select **Roles and access (2)**.

4.  Verify that your user account has one of the following roles:

    -   Data Product Owner
    -   Data Steward
    -   Governance Domain Owner
    -   Global Catalog Reader

> **Important:** Without appropriate governance permissions, you will
> not be able to create or publish Data Products.

## Task 2: Access Unified Catalog and Locate Data Products

In this task, you will navigate to the Data Products section within
Unified Catalog.

1.  From the left navigation pane of the Microsoft Purview portal,
    select **Unified Catalog (1)**.

2.  On the Unified Catalog homepage, locate and select **Data products
    (2)** under governance components.

3.  Review any existing Data Products listed on the page.

## Task 3: Create a New Data Product

In this task, you will create a new Data Product aligned with a business
use case.

1.  On the **Data products (1)** page, click **+ New data product (2)**.

2.  On the Create data product page:

    -   In the **Name (3)** field, enter: **Customer Analytics Data
        Product**
    -   In the **Description (4)** field, enter: "Curated dataset
        supporting customer analytics and reporting use cases."
    -   Under **Governance domain (5)**, select an existing domain
        created earlier in Day 2.

3.  Click **Create (6)**.

The Data Product will be created in Draft state.

## Task 4: Add Assets to the Data Product

In this task, you will add cataloged assets to the Data Product.

1.  Select **Customer Analytics Data Product (1)**.

2.  On the Data Product details page, locate the **Assets section (2)**.

3.  Click **+ Add assets (3)**.

4.  In the asset selection window:

    -   Use the search box (4) to search for available cataloged assets.
    -   Select one or more assets (5).

5.  Click **Add (6)** to associate the assets with the Data Product.

## Task 5: Configure Business Metadata and Ownership

In this task, you will configure ownership and business context for the
Data Product.

1.  While viewing the **Customer Analytics Data Product (1)**, locate
    the **Owner field (2)**.

2.  Click **+ Assign owner (3)**.

3.  Search for and select a user account (4).

4.  Click **Save (5)**.

5.  Optionally configure additional metadata such as tags or glossary
    terms.

## Task 6: Publish and Search the Data Product

In this task, you will publish and validate discoverability.

1.  From the Data Product details page, click **Publish (1)**.

2.  Confirm that the status changes from **Draft** to **Published (2)**.

3.  Use the search bar (3) at the top of the Microsoft Purview portal
    and search for:

    Customer Analytics Data Product

4.  Confirm that:

    -   The Data Product appears in search results.
    -   Associated assets are visible.
    -   Governance Domain is displayed.
    -   Assigned owner is visible.

## Review

In this lab, you have:

-   Verified governance permissions
-   Created a Data Product
-   Added assets to the Data Product
-   Assigned ownership and metadata
-   Published and validated discoverability

You have successfully completed Lab 08 -- Create, manage and search Data
Products and Assets in Unified Catalog.