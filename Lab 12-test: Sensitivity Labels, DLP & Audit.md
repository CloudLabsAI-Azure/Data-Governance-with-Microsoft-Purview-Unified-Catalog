# Day 4 - Lab 12: Sensitivity Labels, DLP & Audit

In this lab, you will implement data protection and compliance controls using Microsoft Purview. You will create and publish sensitivity labels to classify sensitive data, configure Data Loss Prevention (DLP) policies to prevent unauthorized sharing, and apply these controls to datasets in Microsoft Fabric.

You will also enable audit logging to monitor user and administrative activities, and review audit logs to gain visibility into how data is accessed and used across the environment.

This lab demonstrates how Purview provides a unified approach to data security, compliance, and monitoring, ensuring sensitive information is protected while maintaining transparency and accountability.

## Task 1: Create sensitivity labels in Microsoft Purview

In this task, you will create two Sensitivity labels, **Highly-Confidential**, to classify and protect organizational data. These labels define access, apply content markings, and help secure sensitive information while ensuring compliance with organizational policies.

1. In the Microsoft Edge browser window, navigate to the **Microsoft Purview** portal using the URL below:

    ```
    https://purview.microsoft.com/
    ```

1. From the left navigation pane of the Microsoft Purview, click on **Solutions (1)**, select **Information protection (2)**

    ![](./Media/DG500.png)

1. Under **Information protection** panel, select **Sensitivity labels (1)**, and select **Turn on now (2)** in the **yellow** information box that indicate **Your organization has not turned on the ability to process content in Office online files that have encrypted sensitivity labels applied and are stored in OneDrive and SharePoint**.

   > **Note**: Once you do this, there can be a delay for the setting to propagate through the system.

     ![](./Media/DG502.png)

1. On the **Sensitivity labels** page, select **+ Create a label**.

    ![](./Media/DG518.png)

1. On the **Provide basic details for this label** page, enter a **Name**, **Display name**, and **Description for users** as following. Then select **Next (4)** at the bottom of the page:

    - **Name**: Enter the following name **(1)**

       ```
       Highly-Confidential
       ```
    - **Display name** | Enter the following display name **(2)**
        ```
        Highly-Confidential
        ```
    
    - **Description for users** enter the following description **(3)**
        ```
        Highly-Confidential Demo
        ``` 
     
       ![](./Media/DG501.png)

1. Note the scope of this label. The scope is set to **Files and other data assets**, **Emails**, and **Meetings**. Read the description, but don’t change anything. Select **Next** at the bottom of the page.

   ![](./Media/DG503.png)

1. On the **Choose protection settings for the types of items you selected** page, select **Apply content marking (1)**, then select **Next (2)**.

   ![](./Media/DG504.png)
    
1. On the **Content marking** page, take note of the information box at the top of the page. Turn on the **Content Marking (1)** and select the check box for **Add a watermark (2)**, **Add a header (3)**, and **Add a footer (4)**.

   ![](./Media/DG505.png)
   
1. Under **Add a watermark**, click on **Customize text (1)**. Under **Watermark text**, type **Confidential watermark text (2)** and click on **Save (3)**.

   ![](./Media/DG506.png)
  
1. Under **Add a header**, click on **Customize text (1)**. Under **Header text**, type **Confidential Document (2)** and click on **Save (3)**.

   ![](./Media/DG507.png)

1. Under **Add a footer**, click on **Customize text (1)**. Under **Footer text**, type **Confidential Document (2)** and click on **Save (3)**.

   ![](./Media/DG508.png)

   > **Note:** Content markings are applied to documents. For emails, only headers and footers are supported; watermarks are not.

1. Verify **Content marking (1)** settings including watermark, header, and footer, then click **Next (2)**

   ![](./Media/DG509.png)
      
1. You are now in the Auto-labeling for files and emails window. Turn on the **Auto-labeling for files and emails**.

   ![](./Media/DG510.png)
   
1. Read the description of auto-labelling at the top of the page and the information box below it, and under **Detect content that matches these conditions**. Click on **+ Add condition (1)** from the drop-down select **Content contains (2)**

   ![](./Media/DG511.png)
  
1. Then under **Group name** select **Add (1)** drop-down, select **Sensitive info type (2)** and in **Sensitive info type** window search for **Credit (3)** and select the **Credit card number (4)**, select **Add (5)** from the button, select **Next** on the bottom of the page.

   ![](./Media/DG512.png)

   > **Note:** If you did not find sensitive info type groups as mentioned, navigate back to the labels page and ensure that the features have been enabled as specified.

1. On the **Define protection settings for groups and sites** page. Select **Next** at the bottom of the page.

   ![](./Media/DG514.png)
          
1. Review the settings and click on the **Create label**.

   ![](./Media/DG515.png)
      
1. On the **'Your sensitivity label that was created'** blade, select **Don't create a policy yet (1)** and click **Done (2)**.

   ![](./Media/DG516.png)

1. Back on the **Sensitivity labels** blade, notice the newly created sensitivity labels.After creating the label, on the **Labels** page, observe the list of labels you have created.

   ![](./Media/DG517.png)


   > **Note**: Creating Sensitivity labels is essential for maintaining a structured approach to data protection. It allows organizations to clearly define the sensitivity level of their data, enabling the implementation of tailored security measures. This proactive approach helps prevent unauthorized access and ensures compliance with data protection policies.

   > **Note**: Once you have created sensitivity labels in the next lab, you'll configure label policies, and then you can start using them and learn how to manage sensitivity labels. You'll also learn to apply sensitivity labels to emails and files in upcoming labs.

## Task 1.1: Publish the sensitivity label to the user

In this task, you will focus on publishing existing sensitivity labels in Microsoft Purview. The process involves navigating through the Information Protection section and selecting specific labels to be published. This step is crucial for making the defined sensitivity labels accessible and applicable to all users within the organization.

1. Navigate back to the **Microsoft Purview** home page using the URL below.

   ```
   https://purview.microsoft.com/
   ```
1. In Microsoft Purview portal, under **Information Protection**, select **Sensitivity labels (1)** from the panel and click on **Publish labels (2)**.

   ![](./Media/DG600.png)
    
1. Select **Choose sensitivity labels to publish (1)**. A window opens that provides information about the policy. Select **Highly-Confidential (2)** from the list of label and select **Add (3)**.

    ![](./Media/DG601.png) 

1. Back on **Choose sensitivity labels to publish** blade, click on **Next**.

   ![](./Media/DG602.png) 
     
1. Click **Next** on the **Assign admin units** page.

     ![](./Media/DG604.png) 

1. Read the description under **Publish to users and groups**. Notice that this label is available to all users. Do not change any settings. Then select **Next** at the bottom of the page.

    ![](./Media/DG605.png) 

1. Under the **Policy settings**. Select **Require users to apply a label to their Fabric and Power BI content (1)**, then click **Next (2)**

    ![](./Media/DG606.png) 

1. Under the **Apply a Default label to documents**, Select. Select **Next** at the bottom of the page.

    ![](./Media/DG607.png) 

1. Under the **Apply a Default label to emails**, don’t change any settings. Select **Next** at the bottom of the page.

     ![](./Media/DG608.png) 
 
    
1. On the **Default settings for meetings and calendar events**, don’t change any settings. Select **Next** at the bottom of the page.    

   ![](./Media/DG609.png) 

1. Under the **Apply a default label to Fabric and Power BI content**, don’t change any settings. Select **Next** at the bottom of the page.

     ![](./Media/DG610.png)  
    
1. The last configuration option is to name your policy. Enter the policy name as **Highly-Confidentia-Policy (1)**. Then select **Next (2)** at the bottom of the page.

   ![](./Media/DG611.png)    
    
1. Review the settings, click on **Submit**, and then select **Done**.

   ![](./Media/DG612.png)  
    
   ![](./Media/DG613.png)   

1. From the left navigation pane, expand **Policy (1)**, then select **Label publishing policies (2)**. Notice the newly published label policy **Highly-Confidentia-Policy (3)**.

   ![](./Media/DG614.png)   

   >**Note**: Publishing sensitivity labels is essential for ensuring uniform data protection across the organization. Sensitivity labels have now been published and made available to all users, so organizations can enforce consistent policies for handling sensitive information. This step contributes to a cohesive approach to data security and compliance, as it ensures that established sensitivity labels are effectively communicated and applied throughout the user base.
   
   >**Note**: Before starting the validation process for this lab, please be aware that it may take some time for the sensitivity label to take effect. Therefore, we recommend completing the remaining labs first and then proceeding with the validation.

## Task 1.2: Create a Data Loss Prevention (DLP) policy

In this task, you will create a Data Loss Prevention (DLP) policy in the Microsoft Purview portal to prevent sensitive data from being shared.

1. Navigate back to the **Microsoft Purview** home page using the URL below.

   ```
   https://purview.microsoft.com/
   ```

1. In the **Microsoft Purview** portal, in the left navigation pane, click on **Solutions (1)** and select **Data loss prevention (2)**.
   
   ![](./Media/DG800.png)   

1. On the **Policies** page, select **+ Create policy** to start the wizard for creating a new data loss prevention policy.

      ![](./Media/DG801.png) 

1. On the **What info do you want to protect?**, select **Enterprise applications & devices**.

      ![](./Media/DG802.png) 

1. On the **Start with a template or create a custom policy** page, scroll down and select **Custom (1)** under **Categories** and **Custom policy (2)** under **Regulations**. By default, both  options should already be selected. Select **Next (3)**.

   ![](./Media/DG803.png) 
   
1. On the **Name your DLP policy** page, type **Credit card policy (1)** in the **Name** field and type **Protect credit card numbers from being shared. (2)** in the description field. Select **Next (3)**.

      ![](./Media/DG804.png) 

1. On the Assign admin units page, click **Next**.

      ![](./Media/DG805.png) 

1. On the **Choose where to apply the policy** page, 1. Select **Fabric and Power BI workspaces (1)**, then click **Next (2)**

     ![](./Media/DG806.png) 
   
1. On the **Define policy settings** page, select **Create or customize advanced DLP rules** and select **Next**.

      ![](./Media/DG807.png) 

1. On the **Customize advanced DLP rules** page, select **+ Create rule**.

    ![](./Media/DG809.png) 

1. On the **Create rule** page, type **Credit card information** in the **Name** field.

   ![](./Media/DG810.png) 

1. Under **Conditions**, select **+ Add Condition (1)** and then select **Content contains (2)** from the drop-down menu.

   ![](./Media/DG811.png) 

1. In the new **Content contains** page, select **Add (1)** and select **Sensitive info types (2)** from the drop-down menu. On the Sensitive info types page, search **Credit (3)**, select **Credit Card Number (4)**, and select **Add (5)**.

   ![](./Media/DG512.png) 

1. Under **Actions**, click **Add an action (1)** and select **Restrict access or encrypt the content in Microsoft 365 locations (2)** from the drop-down menu.

    ![](./Media/DG812.png) 

1. Under the **Restrict access or encrypt the content in Microsoft 365 locations**, select **Block everyone**.

    ![](./Media/DG813.png) 

1. Under **User notifications**, turn on **Use notifications (1)** and select **Notify users in Office 365 service with a policy tip or email notifications (2)**

   ![](./Media/DG814.png) 

1. Under **Incident reports**, select the **severity level** as **Medium (1)**. Click on the toggle for under **Send an alert to admins when a rule match occurs (2)** and click on **Save (3)**.

    ![](./Media/DG815.png) 

1. Back on the **Customize advanced DLP rules** page, click on **Next**.

    ![](./Media/DG816.png) 

1. On **Policy mode** select **Turn the policy on immediately (1)** and click **Next (2)**.

    ![](./Media/DG817.png) 
  
1. On the Review and Finish page, review the information and click on **Submit**. 
  
      ![](./Media/DG818.png) 

1. Select **Done** on the **New policy created** page.

      ![](./Media/DG819.png) 

   >**Note**: You have now created a DLP policy that scans for Credit Card numbers in Microsoft Outlook.

   >**Note**: Data Loss Prevention policies are critical for organizations to prevent the inadvertent sharing of sensitive information. In this scenario, the focus is on protecting Credit Card numbers. The lab ensures that users are informed and prompted before sharing such data. This proactive approach helps in securing sensitive information and ensures that users are aware of the policy requirements.

## Task 1.3: Configure and Apply Sensitivity Labels  

In this task, you will learn how to enable sensitivity label settings in the **Microsoft Purview Admin portal** and apply a **Highly-Confidential** label to a Fabric semantic model to enforce data protection and governance.

1. Navigate back to fabric portal, select **Settings (1)** from the top right corner and then select **Admin portal (2)**

   ![](./Media/DG700.png)

1. In the **Admin portal**, use the search bar to search for **Sensitivity Labels (1)** and review the **Information protection** section (2)

   ![](./Media/DG701.png)

1. In **Information protection**, select **Allow users to apply sensitivity labels for content (1)** to open the setting

1. Turn on **Enabled (2)**, select **The entire organization (3)**, and click **Apply (4)**

    ![](./Media/DG702.png)

1. Repeat the same steps for all remaining **sensitivity label settings**

1. Once enabled then verify all show **Enabled for the entire organization**

    ![](./Media/DG704.png)

1. In the Fabric portal, select **Workspaces (1)** from the left navigation and open **Purview-Lab (2)**

   ![](./Media/DG708.png)

1. In the workspace, select the **PurviewLakehouse** semantic model

   ![](./Media/DG709.png)

1. Click **Select a label (1)**, open the dropdown (2), and choose **Highly-Confidential (3)**

   ![](./Media/DG710.png)

1. Verify that the **Sensitivity label** is updated to **Highly-Confidential** in the overview

   ![](./Media/DG711.png)

   > **Note:** If the Fabric view is not enabled, select **Power BI (1)** and switch to **Fabric (2)**

   ![](./Media/DG707.png)

   ![](./Media/DG706.png)

## Task 2: Enable audit and monitoring   

> Audit in Microsoft Purview is a centralized logging and monitoring capability that records user and admin activities across services like:

- Microsoft Fabric / Power BI
- Azure Databricks (integrated scenarios)
- SharePoint / OneDrive
- Exchange

> Key Features of Audit

1. Centralized Activity Tracking
    - Tracks actions across multiple services in one place
    - Eliminates need for separate logs
 
2. Detailed Event Logging
    - Captures:
        - View events
        - Create/update/delete actions
        - Sharing and access

3. Advanced Filtering
   - Filter by:
      - User
      - Activity type
      - Date/time
      - Workload (Fabric, Power BI, etc.)

4. Compliance & Security Ready
   - Supports:
      - Regulatory audits
      - Security investigations
      - Insider risk detection

1. In the **Microsoft Purview portal**, click on **Solutions** from the left navigation. Select **Audit**.

   ![Picture 1](./Media/sandbox-purview-image343.png)

1. On the Audit page, click **Start recording user and admin activity**.

    ![Picture 1](./Media/sandbox-purview-image345.png)

3. If prompted with a setup dialog, click **Yes** to complete the organizational setup.

   ![Picture 1](./Media/sandbox-purview-image346.png)

   > **Note:** Audit logging must be enabled before any activity can be tracked.
   
1. In the **Activities - friendly names** field, click the dropdown.

2. Search for `fabric`.

3. Select the following activities:
   - Viewed Power BI dashboard
   - Created Power BI dashboard

    ![Picture 1](./Media/sandbox-purview-image347.png)

1. In the **Users** field, type `odl`.

2. Select the suggested user (e.g., **ODL_User**).

   ![Picture 1](./Media/sandbox-purview-image348.png)
   
1. Under **Date and time range (UTC)**:
   - Set the **Start date**
   - Set the **End date**

2. Click **Search**.

   ![Picture 1](./Media/sandbox-purview-image349.png)

## Task 2.1: Review Audit Results (Read Only)

1. Review the returned audit logs.
2. Observe the following details:
   - Activity name
   - User who performed the action
   - Timestamp
   - Workload (e.g., Power BI / Fabric)

### Expected Outcome

- Audit logging is successfully enabled.
- You can search and view user activities such as:
  - Viewing dashboards
  - Creating dashboards
- Audit results provide visibility into **who performed what action and when**.

## Summary
In this lab, you:

Created and published sensitivity labels to classify and protect critical data
Implemented DLP policies to prevent exposure of sensitive information
Applied labels to Fabric assets and enabled audit logging
Reviewed audit logs to monitor data access, usage, and compliance


## Click Next to continue to the next lab.

![](./Media/sandbox-purview-image342.png)
