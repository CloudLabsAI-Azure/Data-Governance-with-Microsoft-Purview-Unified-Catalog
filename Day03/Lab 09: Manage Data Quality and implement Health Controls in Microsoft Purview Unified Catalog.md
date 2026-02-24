# Day 03 -Lab 09: Manage Data Quality and implement Health Controls in Microsoft Purview Unified Catalog

## Estimated Duration: 120 Minutes

## Lab Overview

In this lab, you will explore how Microsoft Purview Unified Catalog
enables organizations to monitor and manage Data Health and implement
governance Controls.

You will navigate the Data Health experience, configure Health Controls,
define thresholds, and review health dashboards. This lab uses a
demo-based approach to simulate governance monitoring scenarios without
relying on real-time production data.

## Lab Objectives

In this lab, you will perform the following:

-   **Task 1:** Verify Required Roles for Data Health and Controls
-   **Task 2:** Access Data Health and Controls in Unified Catalog
-   **Task 3:** Create a Health Control
-   **Task 4:** Configure Control Thresholds
-   **Task 5:** Review Data Health Dashboard
-   **Task 6:** Simulate Governance Monitoring Scenario

## Task 1: Verify Required Roles for Data Health and Controls

In this task, you will confirm that your account has the necessary
permissions to configure and manage Health Controls.

1.  Open a web browser and navigate to:

    https://purview.microsoft.com

2.  After signing in, from the left navigation pane of the Microsoft
    Purview portal, select **Settings (1)**.

3.  Under Settings, select **Roles and access (2)**.

4.  Verify that your user account has one of the following roles:

    -   Data Steward
    -   Governance Domain Owner
    -   Data Product Owner
    -   Global Catalog Reader (for monitoring visibility)

> **Important:** Without appropriate governance roles, Health Controls
> configuration options may not be visible.

## Task 2: Access Data Health and Controls in Unified Catalog

In this task, you will navigate to the Data Health and Controls section.

1.  From the left navigation pane of the Microsoft Purview portal,
    select **Unified Catalog (1)**.

2.  On the Unified Catalog homepage, locate and select **Data health
    (2)**.

3.  Review the Data Health overview dashboard.

4.  From the Data Health page, locate and select **Controls (3)** to
    view existing governance controls.

## Task 3: Create a Health Control

In this task, you will create a new governance Health Control to monitor
asset completeness.

1.  On the **Controls (1)** page, click **+ New control (2)**.

2.  On the Create control page:

    -   In the **Name (3)** field, enter: **Asset Completeness
        Monitoring**
    -   In the **Description (4)** field, enter: "Monitor completeness
        of metadata and ownership assignment for governed assets."
    -   Under **Governance domain (5)**, select an existing domain from
        Day 3 or previous labs.

3.  Select an applicable control type (6) related to metadata
    completeness or ownership.

4.  Click **Create (7)**.

The control will initially be created in Draft state.

## Task 4: Configure Control Thresholds

In this task, you will configure threshold criteria for the Health
Control.

1.  Select the **Asset Completeness Monitoring (1)** control.

2.  Locate the **Threshold settings (2)** section.

3.  Configure threshold values such as:

    -   Minimum percentage of assets with assigned owners (3) -- for
        example, 80%
    -   Required metadata fields coverage (4)

4.  Save the configuration by clicking **Save (5)**.

> **Note:** Thresholds define acceptable governance standards and
> determine health status indicators.

## Task 5: Review Data Health Dashboard

In this task, you will review how Health Controls reflect in the Data
Health dashboard.

1.  From the left navigation pane, select **Unified Catalog (1)**.

2.  Select **Data health (2)**.

3.  Review the health indicators, including:

    -   Overall health status
    -   Control status
    -   Domain-level health metrics

4.  Select the **Asset Completeness Monitoring (3)** control to review
    its current status.

## Task 6: Simulate Governance Monitoring Scenario

In this task, you will simulate interpreting governance health results.

1.  Assume that asset ownership coverage drops below the configured 80%
    threshold.

2.  Navigate to **Data health (1)** and review how the control status
    reflects warning or risk indicators.

3.  Select the control and review details such as:

    -   Impacted assets
    -   Governance domain
    -   Threshold deviation

4.  Discuss governance remediation actions such as:

    -   Assign missing asset owners
    -   Update metadata completeness
    -   Review domain accountability

> **Scenario Goal:** Understand how Health Controls support proactive
> governance monitoring.

## Review

In this lab, you have:

-   Verified governance permissions
-   Navigated Data Health and Controls
-   Created a Health Control
-   Configured governance thresholds
-   Reviewed the Data Health dashboard
-   Simulated a governance monitoring scenario

You have successfully completed Lab 09 -- Manage Data Quality and
implement Health Controls in Microsoft Purview Unified Catalog.