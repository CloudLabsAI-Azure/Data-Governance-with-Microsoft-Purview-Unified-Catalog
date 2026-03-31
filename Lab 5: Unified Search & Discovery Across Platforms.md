# Lab 5: Unified Search & Discovery Across Platforms

### Task 1: Search Data Assets Across Fabric and Databricks

1. In the Purview portal select Unified Catalog > Discovery > Data assets.

1. In the search bar, search for:
   ```
   dimension_customer
   ```
1. Open the Fabric Lakehouse table and review schema and properties


2. Search for:

   ```
   customer
   ```
1. Select Databricks samples.tpch.customer and review schema

1. Search for:
   - sale → observe results from both Fabric and Databricks
   - orders → observe Databricks results
   - vendors → verify Fabric table

1. Use filters:
 
   - Filter by Source type (Fabric / Azure Databricks Unity Catalog)

1. Expected Result: Assets from both Fabric and Databricks are visible in search results. You can identify differences based on source type

## Task 2: Compare Metadata Completeness

1. Search for dimension_customer → open the Fabric table
   - Review:

      - Schema → Present
      - Description → Missing
      - Owner → Missing
      - Classifications → Present (if applied)

1. Search for customer → open Databricks samples.tpch.customer
   - Review:
     - Schema → Present
     - Description → Present (default from Unity Catalog)
     - Owner → Missing
     - Classifications → Present (if applied)

1. Compare both assets:
   - Fabric → requires manual metadata enrichment
   - Databricks → includes some default metadata

1. Expected Result: You understand differences in metadata availability between Fabric and Databricks

### Task 3: Identify Ownership and Documentation Gaps

1. From previous task observations, identify missing metadata:
      - Description → Missing
      - Owner → Missing
      - Glossary terms → Missing

1. Open Fabric dimension_customer
   - Click Edit and update:
   - Add description
   - Assign Owner
   - Assign Expert

1. Save changes and verify updates on the asset page
1. Attempt to edit Databricks customer
