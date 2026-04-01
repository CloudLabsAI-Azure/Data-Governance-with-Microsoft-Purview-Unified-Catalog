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
3. You should see the **Enterprise glossary (preview)** page with the tabs: **Glossary terms**, **Critical data elements**, **OKRs**
4. On the left, you will see your governance domains listed (e.g., `Sales Analytics` from Lab 6)

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

**Expected Result**: 4 glossary terms created under the `Sales Analytics` governance domain with definitions, approved status, and owners assigned.

---

## Task 2: Publish Terms and Link to Data Products (15 min)

> **How do glossary terms connect to data?** In the Enterprise glossary, terms link to **data products** (not individual assets). Data products contain assets. So the chain is: **Term → Data Product → Assets**. This is by design — it scales governance by applying term policies to entire data products.

**Step 1: Publish Glossary Terms**

> Terms are created in **draft** state and only visible to stewards and domain owners. You must **publish** them to make them visible to all users.

1. Go to **Unified Catalog** → **Catalog management** → **Governance domains** → click `Sales Analytics`
2. On the **Glossary terms** card, click **View all**
3. Click the `Customer` term → on the details page, click **Publish**
4. Repeat for `Revenue`, `Order`, and `Personally Identifiable Information (PII)` — publish all 4 terms

> **Note**: The governance domain (`Sales Analytics`) must already be published (done in Lab 6) before you can publish glossary terms within it.

**Step 2: Link Terms to Data Products from the Glossary Side**

5. Go to **Enterprise glossary** → click on the `Customer` term
6. Click the **Related** tab
7. You will see sections for: **Synonyms**, **Related terms**, **Data products**, **Critical data elements**
8. Click **Add data product** → search for `Customer 360` → select it → click **Add**
9. The `Customer` term is now linked to the `Customer 360` data product

10. Go back to **Enterprise glossary** → click on the `Revenue` term
11. Click **Related** tab → **Add data product** → search `Customer 360` → select → **Add**

12. Repeat for `Order` — link it to `Customer 360` as well

> **Why link to data products?** When a term is linked to a data product, the term's policies (access, health) apply to that data product. Business users browsing the glossary can click through to the data product and see all its assets.

**Step 3: Verify Links from the Data Product Side**

13. Go to **Catalog management** → **Data products** → click `Customer 360`
14. Check the details page — you should see the linked glossary terms (`Customer`, `Revenue`, `Order`)
15. You can also link terms from here: on the data product details page, look for a glossary terms section where you can add or remove linked terms

**Step 4: Understand the Two Glossary Systems**

16. Go to **Data assets** → search for `dimension_customer` → click **Edit**
17. Scroll to the **Glossary terms** section → click **+ Add term**
18. You may see: *"Only DG glossary terms will be shown here after you complete glossary migration."*

    > **What does this mean?** The asset Edit page uses the **Classic glossary** connector. Enterprise glossary terms link to **data products** (via the Related tab), not to individual assets via the Edit page. This is the designed architecture:
    > - **Classic glossary**: terms link directly to individual assets (old pattern)
    > - **Enterprise glossary**: terms link to **data products** which contain assets (new pattern)
    >
    > The "glossary migration" message appears when no Classic glossary terms exist. You can access the Classic glossary via **Catalog management** → **Classic types** → **Glossaries** tab — but for this workshop, we use the Enterprise glossary.

19. Click **Cancel**

    | Feature | Status |
    |---------|--------|
    | Create and publish glossary terms | ✅ Works |
    | Link terms to **data products** (Related tab → Add data product) | ✅ Works |
    | Link terms to other terms (Synonym/Related) | ✅ Works |
    | Link terms to **individual assets** (asset Edit page) | Uses Classic glossary, not Enterprise |
    | Terms appear in search results | ✅ Works |
    | Terms visible on governance domain | ✅ Works |
    | Term policies apply to linked data products | ✅ Works |

**Expected Result**: All 4 glossary terms published. `Customer`, `Revenue`, and `Order` linked to the `Customer 360` data product. The Term → Data Product → Asset governance chain is established.

---

## Task 3: Validate Business-to-Technical Alignment (15 min)

> With glossary terms published and linked to data products, the full governance chain is active. This task validates the end-to-end business-to-technical alignment.

**Step 1: Search for Glossary Terms in Discovery**

1. Go to **Unified Catalog** → **Discovery** → **Data assets**
2. In the search bar, type `Customer` → review results
3. You should see:
   - The `Customer` glossary term in search suggestions or results
   - Data assets with "customer" in their name (`dimension_customer`, Databricks `customer` tables)
4. Business users can discover both the **business definition** (glossary term) and the **technical data** (assets) from the same search. Clicking the glossary term leads to linked data products, which contain the actual assets

**Step 2: Verify Governance Domain Alignment**

5. Go to **Catalog management** → **Governance domains** → click `Sales Analytics`
6. Review the domain page — it should show:
   - **Data products**: `Customer 360` (from Lab 6)
   - **Glossary terms**: `Customer`, `Revenue`, `Order`, `PII` (from this lab)
7. The governance domain ties together: data products + glossary terms
8. When a user browses the `Sales Analytics` domain, they see both the business vocabulary AND the curated data products

**Step 3: Browse by Governance Domain**

9. Go to **Unified Catalog** → **Discovery** → **Browse**
10. Select **By governance domain** → click `Sales Analytics`
11. Review what appears under the domain:
    - `Customer 360` data product
    - Glossary terms associated with the domain
12. Click into `Customer 360` → review the assets inside the data product
13. This is how business users navigate: **Domain → Data Product → Individual Assets**
14. The glossary terms provide the **business vocabulary** that complements the technical assets in the data product

**Step 4: Review the Glossary Term Relationship Features**

15. Go back to **Enterprise glossary** → click `Customer`
16. Click the **Related** tab — try adding related terms:
    - Click **Synonym** or **Related** → add `Order` as a related term (if the Add option is available)
    - Click **Related** → add `Revenue`
17. These term-to-term relationships help build a connected business vocabulary:
    - Customer **is related to** Order (customers place orders)
    - Customer **is related to** Revenue (customer purchases generate revenue)
18. Click the **Data observability** tab — review any available observability metrics for the term

**Step 5: Summary of Current Governance Hierarchy**

19. Document the governance structure built across Labs 6-7:

    ```
    Sales Analytics (Governance Domain)
    ├── Data Products
    │   └── Customer 360
    │       ├── dimension_customer (Fabric Lakehouse)
    │       ├── customer (Azure Databricks)
    │       └── sales_suppliers (Azure Databricks)
    ├── Glossary Terms
    │   ├── Customer
    │   ├── Revenue
    │   ├── Order
    │   └── Personally Identifiable Information (PII)
    └── Quality (from Lab 8)
    ```

20. Key takeaway: The governance domain is the **central organizing structure**. Glossary terms link to data products (which contain assets), creating the full chain: **Term → Data Product → Asset**. This scales governance by letting term policies flow down to data products automatically.

**Expected Result**: Governance hierarchy validated: Domain → Data Products → Assets. Glossary terms linked to data products and searchable in Unified Catalog. Term-to-term relationships explored.

---

## Lab 7 Summary

| Task | What You Did | Key Takeaway |
|------|-------------|--------------|
| 1 | Created 4 glossary terms with definitions | Business glossary defines standard enterprise vocabulary within a governance domain |
| 2 | Published terms and linked to data products | Enterprise glossary terms link to data products (not individual assets) — Term → Data Product → Asset is the designed chain |
| 3 | Validated governance hierarchy and search | Terms are discoverable via search, linked to data products, and visible on the governance domain |

---

## Day 2 Summary

| Lab | Topic | Duration | Key Outcome |
|-----|-------|----------|-------------|
| 5 | Unified Search & Discovery | 50 min | Cross-platform search, metadata comparison, ownership gaps identified |
| 6 | Create and Manage Data Products | 50 min | Governance domain + data product created, published to catalog |
| 7 | Business Metadata & Glossary | 50 min | 4 glossary terms created, preview limitations documented, governance hierarchy validated |
| | **Total** | **150 min (~2.5 hrs)** | |

### What Was Accomplished
- Cross-platform discovery validated across Fabric and Databricks
- Metadata completeness gaps identified and partially addressed
- `Sales Analytics` governance domain with `Customer 360` data product published
- Business glossary established with 4 terms under the `Sales Analytics` domain
- Governance hierarchy connected: Term → Data Product → Asset; glossary terms linked to `Customer 360` data product
- Two glossary systems understood: Enterprise glossary links to data products, Classic glossary links to individual assets
