# Lab 1: Purview Environment Setup & Core Configuration 

### Objective:
Configure Microsoft Purview by validating access roles, organizing governance structure using collections and domains, and enabling the Unified Catalog experience.

### Estimated Duration: 20 minutes

### Task 1: Validate Microsoft Purview Account and Access Roles

In this task, you will verify access to the Microsoft Purview account and confirm that the required roles are assigned.

1. Navigate to the Azure portal > Resource Groups > select your resource group.

1. Open the Microsoft Purview account (purview-{deploymentId}).

1. In the Purview resource blade, review the following:

   - Managed resource group: managed-purview-{deploymentId}
   
   - Managed identity: System-assigned (Enabled)
   
   - Atlas endpoint: https://purview-{deploymentId}.purview.azure.com

1. Select Open Microsoft Purview Governance Portal (opens in a new tab).

1. In the Purview portal. Go to Settings (gear icon) → Roles and permissions

1. Verify your account has the following roles:

   - Purview Data Curator (edit metadata and classifications)
   
   - Purview Data Source Administrator (register and scan data sources)
   
   - Purview Data Reader (browse catalog)
   
   - Collection Admin on the root collection

1. If any role is missing. Navigate to Data Map > Collections > Root Collection

1. Select Role assignments > Add.

1. Assign the missing role to your user account

   **>Note**: Wait 2–3 minutes for role propagation

































===============================================================
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


