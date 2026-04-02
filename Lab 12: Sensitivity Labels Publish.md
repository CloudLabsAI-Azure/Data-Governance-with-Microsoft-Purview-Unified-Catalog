# Lab 12 - Publish sensitivity labels 

### Estimated Duration: 15 Minutes

## Lab Overview 

This lab focuses on publishing existing sensitivity labels in Microsoft Purview. Publishing ensures that defined labels, such as  and Highly-Confidential, are made available to all users within the organization. By doing this, organizations can enforce consistent and standardized data protection measures across files, emails, meetings, and other data assets.

## Lab Objective

In this lab, you will perform the following:
- Task 1: Publish the sensitivity label to the user

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

## Summary

In this lab, you successfully published the Highly-Confidential sensitivity labels using the Highly-Confidentia-Policy label publishing policy. Publishing labels ensures that users across the organization can access and apply these labels consistently, supporting a standardized approach to data protection and compliance.

## Click Next to continue to the next lab.

![](./Media/GS0001.png)