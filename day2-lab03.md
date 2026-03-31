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
5. Create the following term:
   - **Name**: `Customer`
   - **Definition**: `A person or organization that purchases goods or services. In the retail context (Fabric), this includes buying group and category. In the benchmark context (Databricks), this includes market segment and account balance.`
   - **Governance domain**: `Sales Analytics`
   - **Status**: `Approved`
   - **Contacts — Steward**: add your lab user account
6. Click **Create**

7. Create a second term — click **+ New term**:
   - **Name**: `Revenue`
   - **Definition**: `The total income generated from sales transactions before deductions. Calculated from unit price multiplied by quantity, excluding tax and returns.`
   - **Governance domain**: `Sales Analytics`
   - **Status**: `Approved`
   - **Contacts — Steward**: add your lab user account
8. Click **Create**

9. Create a third term — click **+ New term**:
   - **Name**: `Order`
   - **Definition**: `A confirmed request from a customer to purchase one or more items. Includes order date, status, total price, and priority. Tracked across both retail (Fabric fact_order) and benchmark (Databricks tpch.orders) systems.`
   - **Governance domain**: `Sales Analytics`
   - **Status**: `Approved`
   - **Contacts — Steward**: add your lab user account
10. Click **Create**

11. Create a fourth term — click **+ New term**:
    - **Name**: `Personally Identifiable Information (PII)`
    - **Definition**: `Any data that can identify a specific individual, including names, addresses, phone numbers, email addresses, and government-issued identifiers. Subject to data protection regulations.`
    - **Governance domain**: `Sales Analytics`
    - **Status**: `Approved`
    - **Contacts — Steward**: add your lab user account
12. Click **Create**

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
7. Go back → search for `samples.tpch.customer` → click on the **Databricks** version
8. Click **Edit** → **Glossary terms** → **+ Add term** → search `Customer` → select → **Add** → **Save**

**Step 2: Map "Revenue" Term to Sales Assets**

9. Search for `fact_sale` → click on the **Fabric Lakehouse** version
10. Click **Edit** → **Glossary terms** → add `Revenue` → **Save**

**Step 3: Map "Order" Term to Order Assets**

11. Search for `fact_order` → click on the **Fabric Lakehouse** version
12. Click **Edit** → **Glossary terms** → add `Order` → **Save**
13. Search for `samples.tpch.orders` → click on the **Databricks** version
14. Click **Edit** → **Glossary terms** → add `Order` → **Save**

**Step 4: Map "PII" Term to Assets with Sensitive Data**

15. Search for `dimension_employee` → click on the **Fabric Lakehouse** version
16. Click **Edit** → **Glossary terms** → add `Personally Identifiable Information (PII)` → **Save**
17. Search for `dimension_city` → click on the **Fabric Lakehouse** version
18. Click **Edit** → **Glossary terms** → add `Personally Identifiable Information (PII)` → **Save**

**Step 5: Verify Term Mappings**

19. Go to **Enterprise glossary** → click on the `Customer` term
20. On the term detail page, look for **Related assets** or **Linked assets**
21. Verify both `dimension_customer` (Fabric) and `samples.tpch.customer` (Databricks) appear
22. Click on the `Order` term → verify `fact_order` (Fabric) and `samples.tpch.orders` (Databricks) appear

**Expected Result**: 4 glossary terms mapped to 7+ assets across Fabric and Databricks. Each term shows its linked assets. Each asset shows its linked glossary terms.

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
   | Customer | `dimension_customer` | `samples.tpch.customer` | ✅ Yes |
   | Revenue | `fact_sale` | — | ❌ Fabric only |
   | Order | `fact_order` | `samples.tpch.orders` | ✅ Yes |
   | PII | `dimension_employee`, `dimension_city` | — | ❌ Fabric only |

10. Note: `Revenue` and `PII` terms are currently only linked to Fabric assets. In a real environment, you would also link Databricks assets containing revenue or PII data

**Step 4: Verify Governance Domain Alignment**

11. Go to **Catalog management** → **Governance domains** → click `Sales Analytics`
12. Review the domain page:
    - **Data products**: `Customer 360` (from Lab 6)
    - **Glossary terms**: `Customer`, `Revenue`, `Order`, `PII` (from this lab)
13. Everything is now connected: Domain → Data Products → Assets → Glossary Terms
14. This hierarchy enables:
    - Business user searches by glossary term → finds assets
    - Business user browses by domain → finds data products → drills to assets
    - Technical user views asset → sees business context (glossary terms, data product membership)

**Step 5: Review Data Estate Insights Improvement**

15. Go to **Data Estate Insights** → **Assets**
16. Compare with the gaps identified in Lab 5 Task 3:
    - Assets with glossary terms: now 7+ (was 0)
    - Assets with owners: improved (assigned in Lab 5 + data products)
    - Assets with descriptions: improved (assigned in Lab 5 + data products)
17. The governance posture is improving with each lab

**Expected Result**: Business glossary terms serve as a bridge between business concepts and technical assets. Cross-platform term mappings enable searching by business concept. Full governance hierarchy visible: Domain → Data Products → Assets → Glossary Terms.

---

## Lab 7 Summary

| Task | What You Did | Key Takeaway |
|------|-------------|--------------|
| 1 | Created 4 glossary terms with definitions | Business glossary defines standard enterprise vocabulary |
| 2 | Mapped terms to Fabric + Databricks assets | Glossary-to-asset links create business-to-technical alignment |
| 3 | Validated two-way navigation and coverage | Business users find data via glossary; technical users see business context on assets |

---

## Day 2 Summary

| Lab | Topic | Duration | Key Outcome |
|-----|-------|----------|-------------|
| 5 | Unified Search & Discovery | 50 min | Cross-platform search, metadata comparison, ownership gaps identified |
| 6 | Create and Manage Data Products | 50 min | Governance domain + data product created, published to catalog |
| 7 | Business Metadata & Glossary | 50 min | 4 glossary terms created, mapped to 7+ cross-platform assets |
| | **Total** | **150 min (~2.5 hrs)** | |

### What Was Accomplished
- Cross-platform discovery validated across Fabric and Databricks
- Metadata completeness gaps identified and partially addressed
- `Sales Analytics` governance domain with `Customer 360` data product published
- Business glossary established with 4 terms mapped to assets across both platforms
- Full governance hierarchy connected: Domain → Data Products → Assets → Glossary Terms → Classifications
