# Lab 12 - Publish sensitivity labels 

### Estimated Duration: 15 Minutes

## Lab Overview 

This lab focuses on publishing existing sensitivity labels in Microsoft Purview. Publishing ensures that defined labels, such as  and Highly-Confidential, are made available to all users within the organization. By doing this, organizations can enforce consistent and standardized data protection measures across files, emails, meetings, and other data assets.

## Lab Objective

In this lab, you will perform the following:
- Task 1: Publish the sensitivity label to the user
- Task 2: Create a Data Loss Prevention (DLP) policy

### Task 1: Publish the sensitivity label to the user

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

### Task 2: Create a Data Loss Prevention (DLP) policy

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

### Summary

In this lab, you:

- Published sensitivity labels to make them available across the organization  
- Configured a label publishing policy for consistent data protection  
- Enabled sensitivity label usage for Fabric and Power BI content  
- Created a DLP policy to protect sensitive data like credit card numbers  
- Enforced data protection using rules, notifications, and access restrictions  

## Click Next to continue to the next lab.

![](./Media/GS0001.png)