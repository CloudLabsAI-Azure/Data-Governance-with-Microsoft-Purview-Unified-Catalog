# Lab 1: Purview Environment Setup & Core Configuration 

## Objective:

Set up and validate the Microsoft Purview environment by verifying access roles, organizing governance structure using collections and domains, and enabling the Unified Catalog experience.

### Estimated Duration: 20 minutes

### Task 1: Validate Microsoft Purview Account and Access Roles

In this task, you will confirm that your Microsoft Purview account is accessible and that you have the required permissions to perform governance activities.

1. Sign in to the Azure portal using the provided lab credentials.

1. Search for and open your Microsoft Purview account.

1. Launch the Microsoft Purview Governance Portal.

1. Navigate to Settings → Collections.

1. Verify that your user account is assigned appropriate roles such as:

   - Collection Admin
    
   - Data Curator
    
   - Data Reader
    
   - Ensure you have access to the root collection.

Task 2: Configure Collections, Domains, and Ownership Model

In this task, you will organize your data governance structure by creating collections and domains, and assigning ownership roles.

Steps:
Create a Collection

Go to Settings → Collections.

Select + Add collection.

Provide a name (e.g., Fabric-Databricks-Domain).

Set the parent as the root collection.

Create the collection.

Assign Roles

Open the newly created collection.

Add role assignments:

Assign yourself as Collection Admin

Assign yourself as Data Curator

Create a Domain

Navigate to Domains from the left menu.

Select + Create domain.

Provide:

Domain name (e.g., Data Analytics Domain)

Description (optional)

Create the domain.

Assign Domain Ownership

Open the created domain.

Add yourself as the Domain Owner.

Task 3: Enable Unified Catalog Experience

In this task, you will enable and explore the Unified Catalog to centralize data discovery and governance.

Steps:

From the left navigation menu, select Data Catalog.

Enable the Unified Catalog experience if not already enabled.

Explore the catalog interface:

Browse assets

View collections

View domains

Confirm that the created collection and domain are visible.
