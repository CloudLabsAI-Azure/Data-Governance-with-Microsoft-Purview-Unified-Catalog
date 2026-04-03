# Day 4 - Lab 12: Health Management, Classifications & Audit

## Lab Overview

In this lab, you will deep-dive into Purview Health Management to assess governance maturity, review auto-detected classifications for data sensitivity across Fabric and Databricks, and explore Data Estate Insights for governance reporting and audit tracking.

This lab demonstrates how Health Management controls measure governance completeness, how auto-detected classifications identify sensitive data without manual effort, and how Data Estate Insights provide executive-level governance reporting.

## Lab Objectives

In this lab, you will perform the following:

- **Task 1:** Explore Health Management & Governance Controls
- **Task 2:** Deep-Dive into Classifications & Data Sensitivity
- **Task 3:** Data Estate Insights & Audit Review

## Estimated Duration: 50 minutes

> **Prerequisites**: Labs 1–11 completed. Data products published, quality rules executed, governance domains created.

---

## Task 1: Explore Health Management & Governance Controls

In this task, you will navigate Health Management in the Unified Catalog to review governance maturity metrics, health controls, and recommended actions for improving governance posture.

**Step 1: Navigate to Health Management**

1. Navigate to the **Purview portal** (`https://purview.microsoft.com`)
2. Click **Unified Catalog** → **Health management**
3. Review the Health Management overview page

**Step 2: Review Health Controls**

4. Click **Controls** → review governance health metrics:

   | Health Control | What It Measures |
   |---------------|-----------------|
   | Assets with owners | % of assets that have an assigned owner |
   | Assets with descriptions | % of assets that have descriptions |
   | Assets in data products | % of assets packaged in data products |
   | Assets with quality rules | % of assets with quality monitoring |
   | Assets with classifications | % of scanned assets with detected classifications |

5. Click into each control to see which assets meet or miss the control
6. Note the overall health score for each dimension

**Step 3: Review Health Actions**

7. Click **Health management** → **Actions**
8. Review recommended governance improvements:
   - **Add owners** — lists assets without assigned owners
   - **Add descriptions** — lists assets without business descriptions
   - **Add to data products** — lists assets not in any data product
   - **Add quality rules** — lists assets without quality monitoring
9. Click on an action → review the list of assets that need attention
10. Pick one action (e.g., "Add descriptions") → select 1-2 assets → add descriptions to demonstrate the workflow
11. Return to **Controls** → verify the health score improved

**Step 4: Review Data Observability (If Available)**

12. In **Health management**, look for **Data observability**
13. If available, review data freshness monitoring, scan health, and asset discovery trends

---

## Task 2: Deep-Dive into Classifications & Data Sensitivity

In this task, you will review auto-detected classifications across Fabric and Databricks assets, examine column-level PII detection, and understand how classifications serve as the foundation for data sensitivity governance.

**Step 1: Review Classifications Across the Estate**

1. Go to **Unified Catalog** → **Discovery** → **Data assets**
2. Use the **Classification** filter on the left sidebar
3. Review what classifications were auto-detected:

   | Classification | Description | Expected Sources |
   |---------------|-------------|-----------------|
   | Person's Name | Names of people | `dimension_customer`, `dimension_employee` |
   | Phone Number | Phone number patterns | `dimension_customer` |
   | Postal Code | Postal/zip codes | `dimension_city` |
   | Email Address | Email patterns | May appear in some assets |

4. Click on a classification filter → review all assets with that classification

**Step 2: Review Column-Level Classifications**

5. Click on `dimension_customer` (Fabric Lakehouse) → go to the **Schema** tab
6. Review column-level classifications:
   - Each column shows its data type
   - Columns with detected PII show classification tags
7. Click on `dimension_city` → check for postal code classifications

**Step 3: Review Databricks Asset Classifications**

8. Search for `customer` → click on a Databricks customer asset
9. Go to the **Schema** tab → review column-level classifications
10. Compare with Fabric `dimension_customer` — both platforms have PII detected automatically

**Step 4: Classification Summary**

11. Document the classification landscape:

    | Asset | Platform | Classifications Detected |
    |-------|----------|------------------------|
    | `dimension_customer` | Fabric | Person's Name, Phone Number |
    | `dimension_city` | Fabric | Postal Code |
    | `dimension_employee` | Fabric | Person's Name, Email Address |
    | Databricks customer assets | Databricks | Person's Name, Phone Number |

12. Classifications serve as the automatic sensitivity detection layer — they work without additional licensing and provide the foundation for governance decisions

---

## Task 3: Data Estate Insights & Audit Review

In this task, you will review Data Estate Insights dashboards for governance reporting, verify the audit trail for scan and governance activities, and document the current governance posture.

**Step 1: Review Data Estate Insights**

1. Go to **Data Estate Insights** (left sidebar)
2. Review the governance dashboards:

   | Dashboard Section | What It Shows |
   |-------------------|--------------|
   | **Assets** | Total discovered, classified, curated |
   | **Scans** | Scan success rate, frequency, last scan dates |
   | **Classifications** | PII detection coverage, classification distribution |
   | **Stewardship** | % with owners, descriptions, glossary terms |

3. Navigate to the **Assets** section:
   - Total assets discovered (from Fabric + Databricks scans)
   - Assets by source type
   - Growth trend

4. Navigate to the **Scans** section:
   - Scan health for `Contoso-Fabric` and `Contoso-Databricks-UC`
   - Last successful scan dates

**Step 2: Review Scan Activity and Audit Trail**

5. Go to **Data Map** → **Data sources**
6. Click `Contoso-Fabric` → review scan history:
   - Scan dates, status, asset counts
   - Who initiated each scan
   - Duration and errors
7. Click `Contoso-Databricks-UC` → review scan history
8. Each scan run is logged with full audit trail

**Step 3: Governance Posture Summary**

9. Document the current governance posture:

    | Governance Metric | Status |
    |-------------------|--------|
    | Total assets discovered | 30+ |
    | Assets with owners | From Labs 5-10 |
    | Assets with descriptions | From Labs 5-10 |
    | Assets with classifications | Auto-detected across estate |
    | Assets with quality scores | From Labs 8-9 |
    | Published data products | Customer 360, Enterprise Master Data |
    | Governance domains | Sales Analytics |
    | Glossary terms | From Labs 7 and 10 |

---

### Summary

In this lab, you:

- Explored Health Management controls and governance maturity metrics
- Reviewed health actions for improving governance posture
- Deep-dived into auto-detected classifications across Fabric and Databricks
- Examined column-level PII detection on data assets
- Reviewed Data Estate Insights dashboards for governance reporting
- Verified the audit trail for scan and governance activities

## Click Next to continue to the next lab.

![](./Media/sandbox-purview-image342.png)
