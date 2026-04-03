# Day 3 - Lab 10: MDM Integration Scenarios

## Lab Overview

In this lab, you will implement master data management (MDM) governance patterns using Microsoft Purview. You will identify master data entities across Fabric and Databricks, create a Classic glossary term to tag authoritative "golden record" sources, package them into a dedicated data product, and validate that master data is discoverable through the Unified Catalog.

Microsoft Purview does not include a native MDM product. This lab demonstrates how to use Purview as the catalog layer for master data governance — identifying, tagging, and linking authoritative data sources so consumers know which datasets are the trusted golden sources.

## Lab Objectives

In this lab, you will perform the following:

- **Task 1:** Identify MDM-Managed Master Data Sources
- **Task 2:** Register Authoritative Master Data in Purview
- **Task 3:** Link Golden Records to Fabric and Databricks Assets
- **Task 4:** Validate Master Data Discoverability

## Estimated Duration: 40 minutes

> **Prerequisites**: Labs 1–9 completed. Quality rules applied, data products published, glossary terms created.

---

## Task 1: Identify MDM-Managed Master Data Sources

In this task, you will search the Unified Catalog to build a map of where the same business entities (customer, location, product) exist across Fabric and Databricks, identifying which sources should be designated as authoritative.

1. Go to **Purview portal** > **Unified Catalog** > **Discovery** > **Data assets**.

1. Search for **customer** — note all customer-related assets across Fabric and Databricks.

1. Search for **dimension_city** — note location data.

1. Search for **dimension_stock_item** — note product data.

1. You're building a mental map of where the same entity exists in multiple places.

---

## Task 2: Register Authoritative Master Data in Purview

In this task, you will create a Classic glossary term called "Golden Record" to tag authoritative master data sources. Classic glossary terms can be mapped directly to individual assets, making them ideal for tagging golden records at the asset level.

1. Go to **Catalog management** > **Classic types** > **Glossaries** > open **Management Glossary**.

1. Click **+ New term** > **System default** > **Continue**.

1. Create term:
   - **Name**: `Golden Record`
   - **Definition**: `The authoritative, trusted source of truth for a master data entity`

1. Click **Create**.

1. Now go to **Data assets** > search **dimension_customer** > click **Edit**.

1. Under **Glossary terms** dropdown > select **Golden Record** > **Save**.

1. Repeat for **dimension_city** and **dimension_stock_item**.

---

## Task 3: Link Golden Records to Fabric and Databricks Assets

In this task, you will create a dedicated `Enterprise Master Data` data product to package all golden record assets together. This provides a single entry point for consumers to find authoritative master data sources.

1. Go to **Catalog management** > **Data products**.

1. Click **+ New data product**.

1. Fill in:
   - **Name**: `Enterprise Master Data`
   - **Description**: `Collection of golden record master data sources - authoritative sources for Customer, Location, and Product entities`
   - **Governance domain**: `Sales Analytics`
   - **Owner**: your ODL user

1. Click **Create**.

1. Open the data product > click **+ Add assets**.

1. Add: **dimension_customer**, **dimension_city**, **dimension_stock_item**.

1. Click **Publish**.

---

## Task 4: Validate Master Data Discoverability

In this task, you will verify that golden record assets are discoverable through search and data products, and confirm that the master data governance structure is visible in the Unified Catalog.

1. Go to **Discovery** > **Data assets**.

1. Search for **Golden Record** (the glossary term) — verify the 3 golden record assets appear in results.

1. Go to **Discovery** > **Data products** > click **Enterprise Master Data**.

1. Verify all 3 assets are listed inside.

1. Click into **dimension_customer** > verify it shows membership in both **Customer 360** AND **Enterprise Master Data**.

---

### Summary

In this lab, you:

- Identified master data entities (Customer, Location, Product) across Fabric and Databricks
- Created a Classic glossary term "Golden Record" and tagged authoritative assets
- Created and published the `Enterprise Master Data` data product with 3 golden record assets
- Validated master data discoverability through search and data product navigation

## Click Next to continue to the next lab.

![](./Media/GS0001.png)
