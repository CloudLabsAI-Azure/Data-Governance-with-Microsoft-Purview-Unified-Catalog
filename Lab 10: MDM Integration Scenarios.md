## Task 1: Identify MDM-managed master data sources

1. Go to Purview portal > Unified Catalog > Discovery > Data assets

1. Search for customer — note all customer-related assets across Fabric and Databricks

1. Search for dimension_city — note location data

1. Search for dimension_stock_item — note product data

1. You're building a mental map of where the same entity exists in multiple places


## Task 2: Register authoritative master data in Purview

This is about tagging the "golden record" assets. Two approaches:


Approach B — Use Classic glossary terms (better, maps to assets):

Go to Catalog management > Classic types > Glossaries > open Management Glossary
Click + New term > System default > Continue
Create term: Name: Golden Record, Definition: The authoritative, trusted source of truth for a master data entity
Click Create

Now go to Data assets > search dimension_customer > click Edit
Under Glossary terms dropdown > select Golden Record > Save
Repeat for dimension_city and dimension_stock_item

## Task 3: Link golden records to Fabric and Databricks assets

Go to Catalog management > Data products
Click + New data product
Fill in:
Name: Enterprise Master Data
Description: Collection of golden record master data sources - authoritative sources for Customer, Location, and Product entities
Governance domain: Sales Analytics
Owner: your ODL user
Click Create
Open the data product > click + Add assets
Add: dimension_customer, dimension_city, dimension_stock_item
Click Publish


## Task 4: Validate master data discoverability

Go to Discovery > Data assets
Search for Golden Record (if you used glossary term approach) or Authoritative source (if you used description approach)
Verify the 3 golden record assets appear in results
Go to Discovery > Data products > click Enterprise Master Data
Verify all 3 assets are listed inside
Click into dimension_customer > verify it shows membership in both Customer 360 AND Enterprise Master Data
