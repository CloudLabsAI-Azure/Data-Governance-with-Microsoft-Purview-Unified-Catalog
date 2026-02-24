# Day 02 - Lab 04: Create and Manage Governance Domains in Microsoft Purview Unified Catalog

## Estimated Duration: 120 Minutes

## Lab Overview

In this lab, you will create and manage Governance Domains in Microsoft
Purview Unified Catalog. Governance Domains allow organizations to
logically organize governance assets such as data products, glossary
terms, OKRs, and critical data elements aligned with business structure.

You will verify required permissions, create and publish a governance
domain, assign domain owners and stewards, create a subdomain, and
validate the governance hierarchy.

## Lab Objectives

In this lab, you will perform the following:

-   **Task 1:** Verify Required Roles for Governance Domain Management
-   **Task 2:** Create and Publish a Governance Domain
-   **Task 3:** Assign Domain Owners and Stewards
-   **Task 4:** Create and Publish a Subdomain
-   **Task 5:** Validate Governance Domain Hierarchy and Access

## Task 1: Verify Required Roles for Governance Domain Management

In this task, you will verify that your account has the necessary
permissions to create and manage Governance Domains in Microsoft Purview
Unified Catalog.

1.  Open a web browser and navigate to the Microsoft Purview portal by
    entering the following URL:

    https://purview.microsoft.com

2.  After signing in, from the left navigation pane of the Microsoft
    Purview portal, scroll through the available menu options and select
    **Settings (1)** to open configuration and access management
    settings.

3.  Under the Settings section, select **Roles and access (2)** to
    review role assignments within the Purview environment.

4.  On the Roles and access page, verify that your user account is
    assigned one of the following roles:

    -   Governance Domain Creator
    -   Governance Domain Owner
    -   Global Catalog Reader

> **Important:** If Governance Domain Creator is not assigned, the + New
> domain button will not be visible.

### Optional Task: Assign Required Roles (If Roles Are Not Visible)

If you do not see Governance Domain roles or cannot create a new domain,
follow these steps.

#### Step A: Assign Purview Administrator Role in Azure Portal

1.  Open the Azure Portal.
2.  In the Search resources, services, and docs (G+/) (1) box at the
    top, enter **Microsoft Purview accounts (2)** and select it under
    services.
3.  Select your Purview account (3).
4.  From the left navigation pane of the Purview resource, select
    **Access control (IAM) (4)**.
5.  Click **+ Add (5)** and then select **Add role assignment (6)**.
6.  Search for and select **Purview Administrator (7)** and click **Next
    (8)**.
7.  Select your user account (9) and click **Review + Assign (10)**.

Wait 2--5 minutes for role propagation.

#### Step B: Assign Governance Domain Creator Role in Purview Portal

1.  Return to https://purview.microsoft.com.
2.  From the left navigation pane, select **Settings (1)**.
3.  Select **Roles and access (2)**.
4.  Select **Governance Domain Creator (3)**.
5.  Click **+ Add members (4)**.
6.  Select your user account (5) and click **Save (6)**.

Sign out and sign back in to validate access.

## Task 2: Create and Publish a Governance Domain

In this task, you will create and publish a Governance Domain
representing a business unit.

1.  From the left navigation pane of the Microsoft Purview portal,
    select **Unified Catalog (1)** to open the governance experience.

2.  On the Unified Catalog page, select **Governance domains (2)** to
    view the existing domain hierarchy.

3.  Click **+ New domain (3)** to begin creating a new governance
    domain.

4.  On the Create domain page:

    -   Enter **Finance Domain (4)** in the Domain name field.
    -   Enter a meaningful description (5).
    -   Ensure Parent domain (6) is set to the Root domain.

5.  Click **Create (7)**.

6.  After the domain is created in draft state, select the domain and
    click **Publish (8)** to activate it.

> **Important:** Domains must be published before they are visible and
> usable by other users.

## Task 3: Assign Domain Owners and Stewards

In this task, you will assign governance roles within the Finance
Domain.

1.  From the Governance domains page, select **Finance Domain (1)**.

2.  Select the **Roles (2)** tab.

3.  Click **+ Assign role (3)**.

4.  Select **Governance Domain Owner (4)**.

5.  Search for and select the user account (5), then click **Save (6)**.

6.  Repeat the process to assign a **Governance Domain Steward (7)** if
    required.

## Task 4: Create and Publish a Subdomain

In this task, you will create a subdomain under the Finance Domain.

1.  From the Governance domains page, select **Finance Domain (1)**.

2.  Click **+ New domain (2)**.

3.  Enter **Accounts Payable (3)** as the Domain name.

4.  Provide a description (4).

5.  Ensure Parent domain (5) is set to Finance Domain.

6.  Click **Create (6)**.

7.  Select the subdomain and click **Publish (7)**.

## Task 5: Validate Governance Domain Hierarchy and Access

In this task, you will validate that the domain structure and
permissions are correctly configured.

1.  Confirm that **Finance Domain (1)** appears under the Root domain.

2.  Expand Finance Domain to verify that **Accounts Payable (2)**
    appears as a subdomain.

3.  Select Finance Domain and review the **Roles tab (3)** to confirm
    assigned users.

4.  Sign in as a Domain Owner or Steward and verify appropriate access.

## Review

In this lab, you have:

-   Verified governance roles
-   Assigned roles if required
-   Created and published a Governance Domain
-   Assigned Domain Owner and Steward roles
-   Created and published a subdomain
-   Validated governance hierarchy and access

You have successfully completed Lab 04.