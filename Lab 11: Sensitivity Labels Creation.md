# Lab 11 - Configure Sensitive Labels 

### Estimated Duration: 20 Minutes

## Lab Overview 

In this lab, you will learn how to create and configure Sensitivity labels in Microsoft Purview. Sensitivity labels are a key component of data protection within Microsoft 365, enabling organizations to classify and safeguard sensitive information. By applying these labels, you can enforce protection settings such as encryption, access restrictions, and content markings. This ensures that sensitive data remains secure, helps prevent unauthorized access, and supports compliance with organizational and regulatory policies.

## Lab Objective

In this lab, you will perform the following:
- Task 1: Create sensitivity labels in Microsoft Purview

### Task 1: Create sensitivity labels in Microsoft Purview

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


## Task 2: 

1. In the Microsoft Purview portal, select **Settings (1)** from the top right corner and then select **Admin portal (2)**

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

## Summary

In this lab, you learned to create and configure sensitivity labels in Microsoft Purview to classify and protect sensitive data. This process helps ensure data security, compliance, and responsible handling within an organization.

## Click Next to continue to the next lab.

![](./Media/GS0001.png)