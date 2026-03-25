# Day 1 — Lab 4: Foundational Metadata, Classification & Lineage

**Duration**: 50 min

---

## Task 1: Run Initial Scans Across Fabric and Databricks (15 min)

> Before reviewing classifications and lineage, verify that all scans from Labs 2 and 3 completed successfully and review the combined data map.

**Step 1: Verify Fabric Scan Results**

1. Go to **Purview portal** (`https://purview.microsoft.com`) → **Data Map** → **Data sources**
2. Click your Fabric source (`Purview-Fabric`) → **Recent scans**
3. Confirm the scan shows **Completed** status
4. Note the asset count — you should see assets for:
   - Lakehouse tables (dimension_customer, dimension_city, fact_sale, etc.)
   - SQL analytics endpoint views
   - Semantic model (Power BI Dataset)
   - Warehouse items

**Step 2: Verify Databricks Scan Results**

5. Go back to **Data sources** → click your Databricks source (`Purview-Databricks-UC`) → **Recent scans**
6. Confirm the scan shows **Completed** status
7. Note the asset count — you should see assets for:
   - Metastore, catalogs, schemas
   - Tables from `samples.tpch` (customer, orders, lineitem, nation, etc.)
   - Tables from `samples.nyctaxi` (trips)

**Step 3: Review the Combined Data Map**

8. Go to **Data Map** → **Data sources** → view the full map
9. You should see both sources under their respective collections:
   - **Fabric Sources** → `Purview-Fabric`
   - **Databricks Sources** → `Purview-Databricks-UC`
10. Click on each source to see the asset count breakdown
11. Go to **Unified Catalog** → **Discovery** → **Data assets** → search with a blank query or `*`
12. Review the total asset count — assets from both Fabric and Databricks should appear together

    | Source | Expected Assets |
    |--------|----------------|
    | **Fabric** | Lakehouse tables, SQL endpoint views, Semantic model, Warehouse items |
    | **Databricks** | Metastore, catalogs, schemas, tpch tables, nyctaxi tables, workspace |

**Expected Result**: Both Fabric and Databricks scans completed. Combined data map shows assets from both platforms in one view.

---

## Task 2: Apply Built-in Classifications (20 min)

> During scanning, Purview automatically samples data and matches column content against 200+ built-in classification rules (name patterns, address formats, postal codes, etc.). Classifications are metadata labels — no data is moved or copied.

**Step 1: Review Classifications on Fabric Lakehouse Tables**

1. Go to **Unified Catalog** → **Discovery** → **Data assets**
2. Search for `dimension_customer` → click on the **Fabric Lakehouse** table asset
3. Click the **Schema** tab
4. Review the auto-applied classifications on columns:

   | Column | Expected Classification | Why |
   |--------|------------------------|-----|
   | Customer | Person's Name | ML model detects name patterns |
   | Postal Code | U.S. Zipcode or Postal Code | Regex matches postal code format |

   > Not all columns will have classifications. Purview only classifies when the match threshold (60%) is met.

5. Go back → search for `dimension_city` → click the Lakehouse table → **Schema** tab
6. Check for classifications on city-related columns (e.g., City, State Province, Postal Code)
7. Go back → search for `dimension_employee` → **Schema** tab → check for Person's Name on employee name columns

**Step 2: Review Classifications on Databricks Tables**

8. Search for `customer` → find and click the `customer` table from the Databricks `samples.tpch` schema
9. Click the **Schema** tab
10. Review classifications on columns:

    | Column | Expected Classification | Why |
    |--------|------------------------|-----|
    | c_name | Person's Name | ML model detects name patterns |
    | c_address | Person's Address | ML model detects address patterns |
    | c_phone | U.S. Phone Number or Phone Number | Regex matches phone format |

    > The TPC-H `customer` table uses synthetic data. Classifications depend on whether the data meets the 60% match threshold.

11. Go back → search for `nation` (from `samples.tpch`) → **Schema** tab
12. Check if `n_name` has **Country** classification (Bloom Filter based)

**Step 3: Compare Classifications Across Platforms**

13. Compare what Purview found on customer data from both platforms:

    | Classification | Fabric `dimension_customer` | Databricks `tpch.customer` |
    |---------------|---------------------------|---------------------------|
    | Person's Name | Customer column | c_name column |
    | Address | *(may not apply — WWI uses structured fields)* | c_address column |
    | Phone | *(not in WWI customer)* | c_phone column |
    | Postal Code | Postal Code column | *(not in TPC-H — embedded in address)* |

14. Note the classification types:

    | Type | How It Works | Examples |
    |------|-------------|----------|
    | **Machine Learning** | Trained on global datasets, detects patterns | Person's Name, Person's Address |
    | **Regex** | Pattern matching with keywords | Email, SSN, Credit Card, Zipcode |
    | **Bloom Filter** | Dictionary-based matching | World Cities, Country Names |

15. Key insight: Same classification engine, different results — because the data schemas are different. Purview adapts to whatever data it finds.

**Expected Result**: PII classifications visible on both Fabric and Databricks table columns. Cross-platform comparison demonstrates consistent governance.

---

## Task 3: Review Technical Lineage Across Platforms (15 min)

> Purview captures data flow relationships between assets. Fabric lineage shows the 3-layer architecture: Lakehouse → SQL analytics endpoint → Semantic Model. Databricks lineage comes from Unity Catalog system tables.

**Step 1: Fabric Lineage**

1. In **Unified Catalog** → search for `dimension_customer` → click on the **Fabric Lakehouse** table
2. Click the **Lineage** tab
3. Observe the lineage chain:
   - **Lakehouse** (Delta tables) → **SQL analytics endpoint** (SQL views) → **Semantic model** (BI layer)
   - This shows Fabric's 3-layer architecture: storage → SQL → BI
4. Click on connected nodes to see:
   - Source details (artifact type, workspace)
   - Asset properties and scan metadata
5. Go back → search for your Lakehouse name (`Purview-Lakehouse`) → click on it → **Lineage** tab
6. You should see all the tables flowing through to the SQL endpoint and semantic model
   > Richer lineage from Dataflows and Pipelines will be explored in later labs

**Step 2: Databricks Lineage**

7. Search for `tpch.orders` → click on it → **Lineage** tab
8. Review any lineage relationships shown:
   - The `samples` catalog is **read-only reference data**, so lineage may be limited or empty
   - This is expected — lineage requires actual data movement (notebooks writing to tables)
   > Databricks lineage is captured from Unity Catalog system tables. Since we didn't run any notebooks against `samples`, there's no transformation lineage to show.

**Step 3: Cross-Platform Lineage Comparison**

9. Search for `customer` — results should include assets from **both** platforms:
   - **Fabric**: `dimension_customer` (Lakehouse table + SQL analytics endpoint view)
   - **Databricks**: `samples.tpch.customer` (Unity Catalog table)
10. Compare:

    | Attribute | Fabric `dimension_customer` | Databricks `tpch.customer` |
    |-----------|---------------------------|---------------------------|
    | **Source type** | Microsoft Fabric | Azure Databricks Unity Catalog |
    | **Schema style** | Dimensional model (Customer Key, Category, Buying Group) | Benchmark model (c_custkey, c_name, c_mktsegment) |
    | **Classifications** | Person's Name, Postal Code | Person's Name, Address, Phone |
    | **Lineage** | Lakehouse → SQL endpoint → Semantic model | Limited (read-only catalog) |
    | **Collection** | Fabric Sources | Databricks Sources |

11. Key governance takeaway: Different platforms, different schemas, but **one unified catalog** — searchable, classified, and governed from a single place.

**Expected Result**: Fabric lineage shows the 3-layer data flow. Databricks lineage is limited for the read-only `samples` catalog. Cross-platform comparison works.

---

## Lab 4 Summary

| Task | What You Did | Time |
|------|-------------|------|
| 1 | Verified scans across Fabric and Databricks, reviewed combined data map | 15 min |
| 2 | Reviewed built-in classifications on both platforms, compared cross-platform | 20 min |
| 3 | Explored technical lineage for Fabric (3-layer) and Databricks, compared platforms | 15 min |
| | **Total** | **50 min** |

---

## Day 1 Complete

You have successfully:
- Set up Purview with collections, domains, and roles (Lab 1)
- Connected Microsoft Fabric and scanned Lakehouse, Warehouse, and Semantic Model assets (Lab 2)
- Connected Databricks Unity Catalog and scanned the `samples` catalog (Lab 3)
- Verified scan results and reviewed the combined data map (Lab 4)
- Reviewed auto-applied PII classifications across both platforms (Lab 4)
- Explored technical data lineage from Fabric's 3-layer architecture (Lab 4)

**Next**: Day 2 — Governance Domains, Data Products & Business Glossary
