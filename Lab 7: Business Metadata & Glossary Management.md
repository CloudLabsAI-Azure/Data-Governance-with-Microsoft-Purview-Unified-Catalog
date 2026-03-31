# Lab 7: Business Metadata & Glossary Management

**Duration**: 50 minutes
**Day**: 2 — Unified Catalog, Discovery & Data Products

## Objective

Create business glossary terms that define standard enterprise terminology, map those terms to technical assets in both Fabric and Databricks, and validate that business-to-technical alignment is visible in the Unified Catalog.

> **Prerequisites**: Labs 1–6 completed. Governance domain (`Sales Analytics`) and data product (`Customer 360`) created and published.

---

## Task 1: Create Business Glossary Terms (20 min)

> **What is a Business Glossary?** The glossary provides a shared business vocabulary for the organization. Each term defines a business concept (e.g., "Customer", "Revenue", "Order") with a standard definition. When glossary terms are linked to technical assets, business users can find data by searching for business concepts instead of table names.

**Step 1: Navigate to the Glossary**

1. Navigate to the **Purview portal** (`https://purview.microsoft.com`)
2. Click **Unified Catalog** → **Discovery** → **Enterprise glossary**
3. You should see the glossary home page — currently empty

**Step 2: Create Glossary Terms**

4. Click **+ New term**
5. On the **Basic details** step:
   - **Name**: `Customer`
   - **Description**: `A person or organization that purchases goods or services. In the retail context (Fabric), this includes buying group and category. In the benchmark context (Databricks), this includes market segment and account balance.`
   - **Governance domain**: `Sales Analytics`
   - **Owner**: add your lab user account
   - **Expert**: add your lab user account
   - **Status**: `Approved`
   - Leave **Parent term** empty
6. Click **Next** → on **Acronyms**, skip → click **Next** → on **Resources**, skip → click **Next** → on **Custom attributes**, click **Create**

7. Create a second term — click **+ New term**:
   - **Name**: `Revenue`
   - **Description**: `The total income generated from sales transactions before deductions. Calculated from unit price multiplied by quantity, excluding tax and returns.`
   - **Governance domain**: `Sales Analytics`
   - **Owner**: add your lab user account
   - **Status**: `Approved`
8. Click **Next** through Acronyms, Resources → on **Custom attributes**, click **Create**

9. Create a third term — click **+ New term**:
   - **Name**: `Order`
   - **Description**: `A confirmed request from a customer to purchase one or more items. Includes order date, status, total price, and priority. Tracked across both retail (Fabric) and benchmark (Databricks) systems.`
   - **Governance domain**: `Sales Analytics`
   - **Owner**: add your lab user account
   - **Status**: `Approved`
10. Click **Next** through Acronyms, Resources → on **Custom attributes**, click **Create**

11. Create a fourth term — click **+ New term**:
    - **Name**: `Personally Identifiable Information (PII)`
    - **Description**: `Any data that can identify a specific individual, including names, addresses, phone numbers, email addresses, and government-issued identifiers. Subject to data protection regulations.`
    - **Governance domain**: `Sales Analytics`
    - **Owner**: add your lab user account
    - **Status**: `Approved`
12. Click **Next** through Acronyms, Resources → on **Custom attributes**, click **Create**

**Step 3: Verify Glossary Terms**

13. Go to **Unified Catalog** → **Discovery** → **Enterprise glossary**
14. Verify all 4 terms appear:
    - `Customer` — Approved
    - `Revenue` — Approved
    - `Order` — Approved
    - `Personally Identifiable Information (PII)` — Approved
15. Click each term to review its definition, governance domain, and steward

**Expected Result**: 4 glossary terms created under the `Sales Analytics` governance domain with definitions, approved status, and stewards assigned.

---

## Task 2: Map Glossary Terms to Fabric and Databricks Assets (15 min)

> **Why map terms?** Linking glossary terms to assets creates a bridge between business language and technical tables. When a business user searches for "Customer", they find not just the glossary definition but also all linked data assets across all platforms.

**Step 1: Map "Customer" Term to Assets**

1. Go to **Unified Catalog** → **Discovery** → **Data assets**
2. Search for `dimension_customer` → click on the **Fabric Lakehouse** version
3. Click **Edit** (pencil icon)
4. In the **Glossary terms** section, click **+ Add term**
5. Search for `Customer` → select it → click **Add**
6. Click **Save**
7. Go back → search for `sales_suppliers` → click on the **Azure Databricks Table** version
8. Click **Edit** → **Glossary terms** → **+ Add term** → search `Customer` → select → **Add** → **Save**
   > **Note**: If the Databricks asset has no Edit button, it is from the read-only `samples` catalog. In that case, skip this step — Databricks `samples` assets cannot be edited in Purview.

**Step 2: Map "Revenue" Term to Sales Assets**

9. Search for `fact_sale` → click on the **Fabric Lakehouse** version
10. Click **Edit** → **Glossary terms** → add `Revenue` → **Save**

**Step 3: Map "Order" Term to Sales Assets**

11. Search for `fact_sale` → click on the **Fabric Lakehouse** version
12. Click **Edit** → **Glossary terms** → add `Order` → **Save**
> **Note**: Databricks `samples` catalog assets (e.g., `samples.tpch.orders`) are **read-only** in Purview — there is no Edit button. You can only map glossary terms to assets from your custom Databricks catalogs or Fabric assets. In a real environment with your own Databricks catalogs, all assets would be editable.

**Step 4: Map "PII" Term to Assets with Sensitive Data**

14. Search for `vendors` → click on the **Fabric Lakehouse** version (uploaded in Lab 4)
15. Click **Edit** → **Glossary terms** → add `Personally Identifiable Information (PII)` → **Save**
16. Search for `dimension_customer` → click on the **Fabric Lakehouse** version
17. Click **Edit** → **Glossary terms** → add `Personally Identifiable Information (PII)` (in addition to the `Customer` term already linked) → **Save**

**Step 5: Verify Term Mappings**

18. Go to **Enterprise glossary** → click on the `Customer` term
19. On the term detail page, look for **Related assets** or **Linked assets**
20. Verify `dimension_customer` (Fabric) appears as a linked asset
21. Click on the `Revenue` term → verify `fact_sale` (Fabric) appears

**Expected Result**: 4 glossary terms mapped to Fabric assets. Databricks `samples` assets are read-only and cannot be mapped. Each mapped asset shows its linked glossary terms.

---

## Task 3: Validate Business-to-Technical Alignment (15 min)

**Step 1: Search by Glossary Term**

1. Go to **Unified Catalog** → **Discovery** → **Data assets**
2. In the search bar, type `Customer` → review results
3. You should now see:
   - The `Customer` glossary term itself
   - All data assets linked to the `Customer` term: `dimension_customer` (Fabric), `samples.tpch.customer` (Databricks)
   - Other assets with "customer" in their name
4. Note how the glossary term provides **business context** alongside technical search results

**Step 2: Navigate from Glossary to Assets**

5. Go to **Enterprise glossary** → click `Customer`
6. Click on a linked asset (e.g., `dimension_customer` from Fabric)
7. On the asset page, verify:
   - The glossary term `Customer` appears in the asset metadata
   - You can navigate from the glossary term to the asset and back
8. This creates a two-way link: Term ↔ Asset

**Step 3: Validate Cross-Platform Term Coverage**

9. Review the mapping summary:

   | Glossary Term | Fabric Assets | Databricks Assets | Cross-Platform? |
   |--------------|---------------|-------------------|-----------------|
   | Customer | `dimension_customer` | `sales_suppliers` (if editable) | Partial |
   | Revenue | `fact_sale` | — | Fabric only |
   | Order | `fact_sale` | — | Fabric only |
   | PII | `vendors`, `dimension_customer` | — | Fabric only |

10. Note: Databricks `samples` catalog assets are read-only in Purview and cannot have glossary terms mapped. Assets from your custom Databricks catalog (e.g., `sales_suppliers`) may be editable. In production with your own Databricks catalogs, full cross-platform mapping would work

**Step 4: Verify Governance Domain Alignment**

11. Go to **Catalog management** → **Governance domains** → click `Sales Analytics`
12. Review the domain page:
    - **Data products**: `Customer 360` (from Lab 6)
    - **Glossary terms**: `Customer`, `Revenue`, `Order`, `PII` (from this lab)
13. Everything is now connected: Domain → Data Products → Assets → Glossary Terms

**Expected Result**: Business glossary terms serve as a bridge between business concepts and technical assets. Full governance hierarchy visible: Domain → Data Products → Assets → Glossary Terms.


