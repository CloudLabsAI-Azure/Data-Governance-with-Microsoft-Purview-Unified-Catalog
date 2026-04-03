# Day 4 - Lab 11: Data Product Access & Governance Controls [Optional]

## Estimated Duration: 50 minutes

## Lab Overview

In this lab, you will explore access governance in a multi-platform environment using Microsoft Purview. You will review how access policies work across Fabric and Databricks, configure data product access request workflows, and review centralized governance controls through Health Management and Data Estate Insights.

This lab demonstrates how Purview provides centralized governance visibility while each data platform (Fabric, Databricks) manages its own access enforcement. Data products serve as the governed channel for consumers to discover and request data.

## Lab Objectives

In this lab, you will perform the following:

- **Task 1:** Understand Access Governance Across Platforms
- **Task 2:** Configure Data Product Access Requests
- **Task 3:** Centralized Governance Controls Review


## Task 1: Understand Access Governance Across Platforms

In this task, you will review how access control works across Fabric and Databricks, and understand Purview's role as the centralized governance catalog.

**Step 1: Review Policy Capabilities by Source Type**

1. Navigate to the **Purview portal**.
2. Review the access governance model for each platform:

   | Source Type | Access Control Location | Purview Role |
   |------------|------------------------|--------------|
   | Fabric | Managed via Fabric workspace roles | Catalog + discovery + quality |
   | Databricks UC | Managed via Unity Catalog grants | Catalog + discovery |
  
3. In this lab environment, data lives in **Fabric** and **Databricks** both manage their own access. Purview provides centralized cataloging, discovery, and quality monitoring.

**Step 2: Review Fabric Workspace Permissions**

4. Switch to the **Fabric portal** (`https://app.fabric.microsoft.com`)
5. Go to the `Purview-Lab-WS` workspace → click **Manage access**
6. Review current workspace roles:

   | Role | Permissions |
   |------|-------------|
   | Admin | Full control |
   | Member | Read + write |
   | Contributor | Read + write to items |
   | Viewer | Read only |

7. These roles control access to ALL items in the workspace (Lakehouse, SQL endpoint, Semantic Model)

**Step 3: Review Databricks UC Permissions**

8. Switch to the **Databricks workspace**
9. Go to **Catalog** > click `samples` > **Permissions**
10. Review grants > the `samples` catalog is read-only for all workspace users
11. Unity Catalog provides fine-grained access at catalog, schema, and table level

**Step 4: Document the Access Model**

12. Return to the **Purview portal** → **Data assets** → search for `dimension_customer`
13. Click **Edit** → append to **Description**: `Access Control: Managed via Fabric workspace roles on Purview-Lab-WS.`
14. Click **Save**

## Task 2: Configure Data Product Access Requests

In this task, you will explore how data products serve as the governed access path consumers discover products in the Unified Catalog and request access through a structured workflow.

**Step 1: Review Data Product Access Settings**

1. Go to **Unified Catalog** > **Catalog management** > **Data products** > click **`Customer 360`**
2. Look for an **Access** or **Policies** tab on the data product
3. Review what access configuration options are available:
   - Access request workflow
   - Approvers configuration
   - Access policy settings

**Step 2: Review Data Product from Consumer Perspective**

4. Go to **Unified Catalog** > **Discovery** > **Data products**
5. Click `Customer 360` > review what a business consumer sees:
   - **Description**: explains the data product purpose
   - **Owner/Expert**: who to contact with questions
   - **Assets**: list of included tables with quality scores
   - **Governance domain**: `Sales Analytics`
   - **Request access** button (if self-service is enabled)

6. Repeat for `Enterprise Master Data` > review the consumer view


## Task 3: Centralized Governance Controls Review

In this task, you will review the centralized governance controls available in Health Management and Data Estate Insights to understand the overall governance posture.

**Step 1: Review Health Management Controls**

1. Go to **Unified Catalog** → **Health management**
2. Click **Controls** → review governance health metrics:
   - Assets with owners
   - Assets with descriptions
   - Assets in data products
   - Assets with quality rules
   - Assets with classifications

3. Click into each control to see which assets meet or miss the control

**Step 2: Review Health Actions**

4. Click **Health management** → **Actions**
5. Review recommended governance improvements:
   - Assets missing owners
   - Assets without descriptions
   - Assets not in any data product
   - Assets without quality rules
6. These actions guide the governance team on what to curate next

**Step 4: Cross-Platform Governance Summary**

9. Document the governance posture:

   | Governance Layer | Fabric | Databricks |
   |-----------------|--------|------------|
   | Scanning | Sub-item level | Item-level |
   | Classifications | Auto-detected PII | Auto-detected PII |
   | Quality rules | Supported with connection | Supported with connection |
   | Data products | Assets added | Assets added |
   | Access control | Workspace roles | Unity Catalog grants |

### Summary

In this lab, you:

- Reviewed the cross-platform access governance model for Fabric and Databricks
- Explored data product access request workflows in the Unified Catalog
- Reviewed centralized governance controls through Health Management
- Assessed governance posture using Data Estate Insights
- Documented the access governance model across platforms

## Click Next to continue to the next lab.

![](./Media/sandbox-purview-image342.png)
