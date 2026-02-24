# Lab 05: Create and Manage Glossary Terms in Microsoft Purview Unified Catalog

## Estimated Duration: 120 Minutes

## Lab Overview

In this lab, you will create and manage Glossary Terms in Microsoft
Purview Unified Catalog. A glossary provides a centralized business
vocabulary that defines data-related terminology across the
organization. Glossary terms help establish consistent definitions,
ownership, and governance alignment for data assets.

This lab is fully independent and does not rely on previous labs. You
will create a glossary, add business terms, assign owners, publish the
glossary, and validate its visibility within Unified Catalog.

## Lab Objectives

In this lab, you will perform the following:

-   **Task 1:** Verify Required Roles for Glossary Management
-   **Task 2:** Access Unified Catalog and Create a New Glossary
-   **Task 3:** Create and Define Glossary Terms
-   **Task 4:** Assign Term Owners and Stewards
-   **Task 5:** Publish the Glossary
-   **Task 6:** Validate Glossary Visibility and Search

## Task 1: Verify Required Roles for Glossary Management

In this task, you will verify that your account has the appropriate
permissions to create and manage glossary terms.

1.  Open a web browser and navigate to the Microsoft Purview portal:

    https://purview.microsoft.com

2.  After signing in, from the left navigation pane, select **Settings
    (1)**.

3.  Under Settings, select **Roles and access (2)**.

4.  Verify that your user account has one of the following roles:

    -   Data Steward
    -   Governance Domain Owner
    -   Glossary Contributor (if available)
    -   Global Catalog Reader (for visibility)

> **Important:** Without appropriate glossary or stewardship
> permissions, you will not be able to create or publish glossary terms.

### Optional Task: Assign Required Roles (If Glossary Roles Are Not Visible)

If glossary roles are not visible or you cannot create a glossary:

#### Step A: Assign Purview Administrator Role in Azure Portal

1.  Open the Azure Portal.
2.  In the Search resources, services, and docs (G+/) (1) box, enter
    **Microsoft Purview accounts (2)** and select it.
3.  Select your Purview account (3).
4.  From the left navigation pane, select **Access control (IAM) (4)**.
5.  Click **+ Add (5)** → **Add role assignment (6)**.
6.  Select **Purview Administrator (7)**.
7.  Assign to your user account (8).
8.  Click **Review + Assign (9)**.

Wait a few minutes for role propagation.

#### Step B: Assign Data Steward Role in Purview Portal

1.  Return to https://purview.microsoft.com.
2.  Select **Settings (1)** → **Roles and access (2)**.
3.  Select **Data Steward (3)**.
4.  Click **+ Add members (4)**.
5.  Select your user account (5).
6.  Click **Save (6)**.

Sign out and sign back in to validate access.

## Task 2: Access Unified Catalog and Create a New Glossary

In this task, you will create a new glossary within Unified Catalog.

1.  From the left navigation pane of the Microsoft Purview portal,
    select **Unified Catalog (1)**.

2.  On the Unified Catalog homepage, select **Glossaries (2)** to view
    existing glossaries.

3.  Click **+ New glossary (3)** to begin creating a new glossary.

4.  On the Create glossary page:

    -   Enter **Enterprise Business Glossary (4)** as the Glossary name.
    -   Provide a meaningful description (5), such as: "Centralized
        glossary containing standardized business data definitions."

5.  Click **Create (6)**.

## Task 3: Create and Define Glossary Terms

In this task, you will create new glossary terms within the Enterprise
Business Glossary.

1.  Select the newly created **Enterprise Business Glossary (1)**.

2.  Click **+ New term (2)**.

3.  On the Create term page:

    -   Enter **Customer ID (3)** as the Term name.
    -   In the Definition field (4), enter: "A unique identifier
        assigned to each customer in the organization."
    -   Optionally add Acronyms or Abbreviations (5), such as CID.

4.  Under the Domain section (6), optionally assign a governance domain
    if available.

5.  Click **Create (7)**.

6.  Repeat the process to create additional terms such as:

    -   Revenue
    -   Invoice Number
    -   Employee ID

## Task 4: Assign Term Owners and Stewards

In this task, you will assign ownership to a glossary term.

1.  Select the term **Customer ID (1)**.

2.  On the term details page, locate the **Owners (2)** or **Stewards
    (3)** section.

3.  Click **+ Add owner (4)**.

4.  Search for and select a user account (5).

5.  Click **Save (6)**.

> **Note:** Assigning owners ensures accountability and governance
> ownership for each term.

## Task 5: Publish the Glossary

In this task, you will publish the glossary to make it available across
the organization.

1.  From within the **Enterprise Business Glossary (1)**, review the
    glossary status indicator.

2.  Click **Publish (2)** to make the glossary active.

> **Important:** Glossary terms must be published before they become
> visible to all users in Unified Catalog.

## Task 6: Validate Glossary Visibility and Search

In this task, you will validate that the glossary and its terms are
searchable and visible.

1.  From the top search bar within the Microsoft Purview portal (1),
    enter **Customer ID (2)**.

2.  Review the search results and confirm that the glossary term
    appears.

3.  Select the term to verify:

    -   Definition is visible
    -   Assigned owners are listed
    -   Glossary association is displayed

4.  Optionally sign in as a Global Catalog Reader to confirm visibility.

## Review

In this lab, you have:

-   Verified glossary-related roles
-   Created a new business glossary
-   Added and defined glossary terms
-   Assigned term ownership
-   Published the glossary
-   Validated glossary visibility and search

You have successfully completed Lab 05: Create and Manage Glossary Terms
in Microsoft Purview Unified Catalog.