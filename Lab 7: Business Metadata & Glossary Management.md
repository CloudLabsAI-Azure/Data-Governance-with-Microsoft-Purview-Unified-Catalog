# Lab 7: Business Metadata & Glossary Management

## Lab Overview

In this lab, you will create and manage business glossary terms in Microsoft Purview to establish a standardized business vocabulary. You will define glossary terms, map them to data assets across Microsoft Fabric and Azure Databricks, and validate how business terminology aligns with technical data assets in the Unified Catalog.

This lab demonstrates how business glossary terms act as a bridge between business concepts and technical metadata, enabling improved data discovery and governance across platforms.

## Lab Objectives

In this lab, you will perform the following:

- **Task 1:** Create Business Glossary Terms  
- **Task 2:** Map Glossary Terms to Fabric and Databricks Assets  
- **Task 3:** Validate Business-to-Technical Alignment  

## Estimated Duration 50 minutes

## Task 1: Create Business Glossary Terms

In this task, you will learn how to create business glossary terms in **Microsoft Purview** to define key business concepts and establish a shared vocabulary.

> **What is a Business Glossary?** The glossary provides a shared business vocabulary for the organization. Each term defines a business concept (e.g., "Customer", "Revenue", "Order") with a standard definition. When glossary terms are linked to technical assets, business users can find data by searching for business concepts instead of table names.

**Step 1: Navigate to the Glossary**

1. Navigate back to the **Microsoft Purview** home page using the URL below.

   ```
   https://purview.microsoft.com/
   ```

1. From the left navigation pane, click **Solutions (1)**, then select **Unified Catalog (2)**.

   ![Picture 1](./Media/DG13.png)

1. Under **Unified Catalog**, expand **Catalog management (1)**, select **Governance domains (2)**, choose **Sales Analytics (3)**, and click **View all (4)** under **Glossary terms**.

   ![Picture 1](./Media/DG79.png)

1. You should see the **Glossary terms** page for the **Sales Analytics** domain, which is currently empty.

   ![Picture 1](./Media/DG80.png)

**Step 2: Create Glossary Terms**

1. Click **+ New term**

   ![Picture 1](./Media/DG81.png)

1. On the **Basic details** step, enter the following:

      | Field | Value |
      |------|------|
      | Name | Customer **(1)** |
      | Description | A person or organization that purchases goods or services. In the retail context (Fabric), this includes buying group and category. In the benchmark context (Databricks), this includes market segment and account balance. **(2)** |
      | Owner | ODL_User<inject key="DeploymentID" enableCopy="false"/> **(3)** |
      | Expert | ODL_User<inject key="DeploymentID" enableCopy="false"/> **(4)** |
      | Parent term | Leave empty |

      ![Picture 1](./Media/DG82.png)

1. Click **Next**, skip Acronyms, Resources, and Custom attributes, then click **Create**

   ![Picture 1](./Media/DG92.png)

1. After creation, click **Publish**

   ![Picture 1](./Media/DG86.png)

1. Click **Glossary terms** at the top left to go back and add a new term

   ![Picture 1](./Media/DG91.png)

1. Click **+ New term**

   ![Picture 1](./Media/DG81.png)

1. On the **Basic details** step, enter the following:

      | Field | Value |
      |------|------|
      | Name | Revenue **(1)** |
      | Description | The total income generated from sales transactions before deductions. Calculated from unit price multiplied by quantity, excluding tax and returns. **(2)** |
      | Owner | ODL_User<inject key="DeploymentID" enableCopy="false"/> **(3)** |
      | Expert | ODL_User<inject key="DeploymentID" enableCopy="false"/> **(4)** |
      | Parent term | Leave empty |

      ![Picture 1](./Media/DG83.png)

1. Click **Next**, skip Acronyms, Resources, and Custom attributes, then click **Create**

   ![Picture 1](./Media/DG92.png)

1. After creation, click **Publish**

   ![Picture 1](./Media/DG88.png)

1. Click **Glossary terms** at the top left to go back and add a new term

   ![Picture 1](./Media/DG91.png)

1. Click **+ New term**

   ![Picture 1](./Media/DG81.png)

1. On the **Basic details** step, enter the following:

      | Field | Value |
      |------|------|
      | Name | Order **(1)** |
      | Description | A confirmed request from a customer to purchase one or more items. Includes order date, status, total price, and priority. Tracked across both retail (Fabric) and benchmark (Databricks) systems. **(2)** |
      | Owner | ODL_User<inject key="DeploymentID" enableCopy="false"/> **(3)** |
      | Expert | ODL_User<inject key="DeploymentID" enableCopy="false"/> **(4)** |
      | Parent term | Leave empty |

      ![Picture 1](./Media/DG84.png)

1. Click **Next**, skip Acronyms, Resources, and Custom attributes, then click **Create**

   ![Picture 1](./Media/DG92.png)

1. After creation, click **Publish**

   ![Picture 1](./Media/DG87.png)

1. Click **Glossary terms** at the top left to go back and add a new term

   ![Picture 1](./Media/DG91.png)

1. Click **+ New term**

   ![Picture 1](./Media/DG81.png)

1. On the **Basic details** step, enter the following:

      | Field | Value |
      |------|------|
      | Name | Personally Identifiable Information (PII) **(1)** |
      | Description | Any data that can identify a specific individual, including names, addresses, phone numbers, email addresses, and government-issued identifiers. Subject to data protection regulations. **(2)** |
      | Owner | ODL_User<inject key="DeploymentID" enableCopy="false"/> **(3)** |
      | Expert | ODL_User<inject key="DeploymentID" enableCopy="false"/> **(4)** |
      | Parent term | Leave empty |

      ![Picture 1](./Media/DG85.png)

1. Click **Next**, skip Acronyms, Resources, and Custom attributes, then click **Create**

   ![Picture 1](./Media/DG92.png)

1. After creation, click **Publish**

   ![Picture 1](./Media/DG89.png)

**Step 3: Verify Glossary Terms**

1. Verify that all created glossary terms show the **Status** as Published

    - `Customer` — Published
    - `Revenue` — Published
    - `Order` — Published
    - `Personally Identifiable Information (PII)` — Published

       ![Picture 1](./Media/DG90.png)

### Management Glossary - via clasic Types option 

1. Navigate back to the **Microsoft Purview** home page using the URL below.

   ```
   https://purview.microsoft.com/
   ```

1. From the left navigation pane, click **Solutions (1)**, then select **Unified Catalog (2)**.

   ![Picture 1](./Media/DG13.png)

1. Under **Unified Catalog** expand **Catalog management (1)** then click **Classic types (2)** and select **+ New glossary (3)**

   ![Picture 1](./Media/DG97.png)

1. On the **New glossary** page, enter the following and click **Create (5)**

      | Field | Value |
      |------|------|
      | Name | Management Glossary **(1)** |
      | Domain | purview-<inject key="DeploymentID" enableCopy="false"/> (Default) **(2)** |
      | Steward | ODL_User<inject key="DeploymentID" enableCopy="false"/> **(3)** |
      | Expert | ODL_User<inject key="DeploymentID" enableCopy="false"/> **(4)** |

      ![Picture 1](./Media/DG98.png)

1. Open the created glossary and click **View terms**

   ![Picture 1](./Media/DG99.png)

1. Click **+ New term (1)** and select **System default** then click **Continue (2)**

   ![Picture 1](./Media/DG100.png)

1. On the **Overview** page, enter the following and click **Create (3)**

      | Field | Value |
      |------|------|
      | Name | Customer **(1)** |
      | Definition | A person or organization that purchases goods or services. In the retail context (Fabric), this includes buying group and category. In the benchmark context (Databricks), this includes market segment and account balance. **(2)** |

      ![Picture 1](./Media/DG101.png)

1. Click **Terms** at the top left to go back and add a new term

   ![Picture 1](./Media/DG105.png)

1. Click **+ New term (1)** and select **System default** then click **Continue (2)**

   ![Picture 1](./Media/DG100.png)

1. On the **Overview** page, enter the following and click **Create (3)**

      | Field | Value |
      |------|------|
      | Name | Revenue **(1)** |
      | Definition | The total income generated from sales transactions before deductions. Calculated from unit price multiplied by quantity, excluding tax and returns. **(2)** |

      ![Picture 1](./Media/DG102.png)

1. Click **Terms** at the top left to go back and add a new term

   ![Picture 1](./Media/DG105.png)

1. Click **+ New term (1)** and select **System default** then click **Continue (2)**

   ![Picture 1](./Media/DG100.png)

1. On the **Overview** page, enter the following and click **Create (3)**

      | Field | Value |
      |------|------|
      | Name | Order **(1)** |
      | Definition | A confirmed request from a customer to purchase one or more items. Includes order date, status, total price, and priority. Tracked across both retail (Fabric) and benchmark (Databricks) systems. **(2)** |

      ![Picture 1](./Media/DG103.png)

1. Click **Terms** at the top left to go back and add a new term

   ![Picture 1](./Media/DG105.png)

1. Click **+ New term (1)** and select **System default** then click **Continue (2)**

   ![Picture 1](./Media/DG100.png)

1. On the **Overview** page, enter the following and click **Create (3)**

      | Field | Value |
      |------|------|
      | Name | Personally Identifiable Information (PII) **(1)** |
      | Definition | Any data that can identify a specific individual, including names, addresses, phone numbers, email addresses, and government-issued identifiers. Subject to data protection regulations. **(2)** |

      ![Picture 1](./Media/DG104.png)

## Task 2: Map Glossary Terms to Fabric and Databricks Assets

In this task, you will learn how to map business glossary terms to **Fabric** and **Databricks** assets in **Microsoft Purview** to connect business context with technical data.

**Step 1: Map "Customer" Term to Assets**

1. From the **Unified Catalog** page, expand **Discovery (1)**, select **Data assets (2)**, search for **dimension_customer (3)**, and then select the **dimension_customer asset (4)**.

   ![Picture 1](./Media/DG44.png)

1. Click **Edit**

   ![Picture 1](./Media/DG106.png)

1. Click the dropdown under **Glossary terms (1)** and select **Customer (2)**

   ![Picture 1](./Media/DG107.png)

1. Verify that **Customer** appears under selected terms, then click **Save (2)**

   ![Picture 1](./Media/DG108.png)

1. Review that **Customer** is displayed under **Glossary terms** in the asset overview

   ![Picture 1](./Media/DG109.png)


1. Click **Data assets (1)**, search for **sales_suppliers (2)**, and select the asset **sales_suppliers (3)**

   ![Picture 1](./Media/DG200.png)

1. Click **Edit**

   ![Picture 1](./Media/DG201.png)

1. Click the dropdown under **Glossary terms (1)** and select **Customer (2)**
   ![Picture 1](./Media/DG202.png)

1. Verify **Customer** is added under selected terms, then click **Save (2)**

   ![Picture 1](./Media/DG203.png)

1. Review that **Customer** appears under **Glossary terms** in the asset overview

   ![Picture 1](./Media/DG204.png)

**Step 2: Map "Revenue" Term to Sales Assets**

1. Click **Data assets (1)**, search for **fact_sale (2)**, and select the asset **fact_sale (3)**

   ![Picture 1](./Media/DG205.png)

1. Click **Edit**

   ![Picture 1](./Media/DG206.png)

1. Click the dropdown under **Glossary terms (1)** and select **Revenue (2)**
   ![Picture 1](./Media/DG207.png)

1. Verify **Revenue** is added under selected terms, then click **Save (2)**

   ![Picture 1](./Media/DG208.png)

1. Review that **Revenue** appears under **Glossary terms** in the asset overview

   ![Picture 1](./Media/DG209.png)

**Step 3: Map "Order" Term to Sales Assets**

1. Click **Data assets (1)**, search for **fact_sale (2)**, and select the asset **fact_sale (3)**

   ![Picture 1](./Media/DG205.png)

1. Click **Edit**

   ![Picture 1](./Media/DG206.png)

1. Click the dropdown under **Glossary terms (1)** and select **Order (2)**
  
   ![Picture 1](./Media/DG300.png)

1. Verify **Order** is added under selected terms, then click **Save (2)**

   ![Picture 1](./Media/DG301.png)

1. Review that **Revenue and Order** appears under **Glossary terms** in the asset overview

   ![Picture 1](./Media/DG302.png)

**Step 4: Map "PII" Term to Assets with Sensitive Data**

1. Click **Data assets (1)**, search for **vendors (2)**, and select the asset **vendors (3)**

   ![Picture 1](./Media/DG205.png)

1. Click **Edit**

   ![Picture 1](./Media/DG206.png)

1. Click the dropdown under **Glossary terms (1)** and select **Personally Identifiable Information (PII) (2)**
  
   ![Picture 1](./Media/DG300.png)

1. Verify **Personally Identifiable Information (PII)** is added under selected terms, then click **Save (2)**

   ![Picture 1](./Media/DG301.png)

1. Review that **Personally Identifiable Information (PII)** appears under **Glossary terms** in the asset overview

   ![Picture 1](./Media/DG302.png)

**Step 5: Verify Term Mappings**

1. Go to **Enterprise glossary** → click on the `Customer` term
1. On the term detail page, look for **Related assets** or **Linked assets**
1. Verify `dimension_customer` (Fabric) appears as a linked asset
1. Click on the `Revenue` term → verify `fact_sale` (Fabric) appears

**Expected Result**: 4 glossary terms mapped to Fabric assets. Databricks `samples` assets are read-only and cannot be mapped. Each mapped asset shows its linked glossary terms.

## Task 3: Validate Business-to-Technical Alignment

In this task, you will learn how to validate business-to-technical alignment in **Microsoft Purview** by exploring glossary-linked assets and cross-platform relationships.

**Step 1: Search by Glossary Term**

1. Go to **Unified Catalog** → **Discovery** → **Data assets**
1. In the search bar, type `Customer` → review results
1. You should now see:
   - The `Customer` glossary term itself
   - All data assets linked to the `Customer` term: `dimension_customer` (Fabric), `samples.tpch.customer` (Databricks)
   - Other assets with "customer" in their name
1. Note how the glossary term provides **business context** alongside technical search results

**Step 2: Navigate from Glossary to Assets**

1. Go to **Enterprise glossary** → click `Customer`
1. Click on a linked asset (e.g., `dimension_customer` from Fabric)
1. On the asset page, verify:
   - The glossary term `Customer` appears in the asset metadata
   - You can navigate from the glossary term to the asset and back
1. This creates a two-way link: Term ↔ Asset

**Step 3: Validate Cross-Platform Term Coverage**

1. Review the mapping summary:

   | Glossary Term | Fabric Assets | Databricks Assets | Cross-Platform? |
---|
   | Customer | `dimension_customer` | `sales_suppliers` (if editable) | Partial |
   | Revenue | `fact_sale` | — | Fabric only |
   | Order | `fact_sale` | — | Fabric only |
   | PII | `vendors`, `dimension_customer` | — | Fabric only |

1. Note: Databricks `samples` catalog assets are read-only in Purview and cannot have glossary terms mapped. Assets from your custom Databricks catalog (e.g., `sales_suppliers`) may be editable. In production with your own Databricks catalogs, full cross-platform mapping would work

**Step 4: Verify Governance Domain Alignment**

1. Go to **Catalog management** → **Governance domains** → click `Sales Analytics`
1. Review the domain page:
    - **Data products**: `Customer 360` (from Lab 6)
    - **Glossary terms**: `Customer`, `Revenue`, `Order`, `PII` (from this lab)
1. Everything is now connected: Domain → Data Products → Assets → Glossary Terms

## Summary

In this lab, you created business glossary terms in Microsoft Purview, mapped them to data assets across Microsoft Fabric and Azure Databricks, and validated the alignment between business concepts and technical metadata. You also explored how glossary terms enhance data discovery and establish a unified governance framework within the Unified Catalog.

## Click Next to continue to the next lab.

![](./Media/GS0001.png)