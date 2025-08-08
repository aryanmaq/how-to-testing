## CI/CD Configuration Guide

### CI/CD Setup Steps

This guide provides a structured approach for configuring and executing a CI/CD pipeline to automate Page Load Time (PLT) testing for Power BI reports.

We have integrated CI/CD to eliminate several manual steps previously performed through the LoadFAST UI---such as creating a collection, defining a test, and triggering it. With this integration, all these actions are now handled automatically within a single workflow, initiated by pipeline execution. This enhancement streamlines the testing process and minimizes human intervention.

**Step 1: Establish a Service Connection in Azure DevOps**

To enable secure access to Azure resources, configure a Service Connection using **Managed Identity** under the **Azure Resource Manager** category.

Procedure:

1.  Open your Azure DevOps **Project Settings**.<figure><img src="../.gitbook/assets/Picture1.png" alt="Go to Admin Settings"><figcaption></figcaption></figure>
<br>

2.  Within the **Pipelines** section, access **Service connections**.<figure><img src="../.gitbook/assets/Picture2.png" alt="Service connections"><figcaption></figcaption></figure>
<br>

3.  Click on the **New service connection** button.<figure><img src="../.gitbook/assets/Picture3.png" alt="New service connection"><figcaption></figcaption></figure>
<br>

4.  Choose **Azure Resource Manager** as the connection type.<figure><img src="../.gitbook/assets/Picture4.png" alt="Azure Resource Manager"><figcaption></figcaption></figure>
<br>

5.  Select **Managed Identity** as the identity type.<figure><img src="../.gitbook/assets/Picture5.png" alt="Managed Identity"><figcaption></figcaption></figure>
<br>

6.  **Configure the Connection:**

- **Subscription:** Select your Azure subscription.

- **Resource Group:** Choose the managed resource group where the LoadFAST was initially deployed and where the Azure Key Vault is located.

- **Managed Identity:** Select the appropriate identity that is associated with the resource group where the LoadFAST tool was deployed.

- **Service Connection Name**: Assign a descriptive name(e.g.,Pipeline_ServiceConnection).

> ***Note:** If you are unsure about the subscription, resource group, or managed identity to select, please contact the administrator who configured or deployed the LoadFAST tool.*

<figure><img src="../.gitbook/assets/Picture6.png" alt="Configure Connection"><figcaption></figcaption></figure>
<figure><img src="../.gitbook/assets/Picture7.png" alt="Configure Connection"><figcaption></figcaption></figure>

7.  Finalize the setup by selecting **Save**.

**Step 2: Configure a Variable Group and Integrate Azure Key Vault**

To manage sensitive credentials securely (e.g., clientId, clientSecret), create a Variable Group and associate it with your Azure Key Vault.

Procedure:

1.  Navigate to the **Library** section within the **Pipelines** menu of your Azure DevOps project.<figure><img src="../.gitbook/assets/Picture8.png" alt="Library Section"><figcaption></figcaption></figure>

2.  Create a new variable group by selecting **+ Variable group**.<figure><img src="../.gitbook/assets/Picture9.png" alt="Add Variable Group"><figcaption></figcaption></figure>

3.  Define the following:

- **Name**: Specify a clear group name, e.g., Pipeline_SecretGroup.

- **Description** (optional): Provide a summary of the group's purpose.<figure><img src="../.gitbook/assets/Picture10.png" alt="Variable Group Description"><figcaption></figcaption></figure>

4.  Enable the option **Link secrets from an Azure key vault as variables**.<figure><img src="../.gitbook/assets/Picture11.png" alt="Link Azure Key Vault"><figcaption></figcaption></figure>

5.  Under **Azure subscription**, choose the service connection configured in Step 1.<figure><img src="../.gitbook/assets/Picture12.png" alt="Choose Service Connection"><figcaption></figcaption></figure>

6.  Select the **Key Vault** which has your clientId and clientSecret.<figure><img src="../.gitbook/assets/Picture13.png" alt="Select Key Vault"><figcaption></figcaption></figure>

7.  Use the **+ Add** option to include **clientId** and **clientSecret**.<figure><img src="../.gitbook/assets/Picture14.png" alt="Add clientId and clientSecret"><figcaption></figcaption></figure>
<figure><img src="../.gitbook/assets/Picture15.png" alt="Add clientId and clientSecret"><figcaption></figcaption></figure>

8.  Select **Save** to complete the configuration.<figure><img src="../.gitbook/assets/Picture16.png" alt="Save Variable Group"><figcaption></figcaption></figure>

**Step 3: Configure and Execute the Pipeline**

This step involves setting up the necessary files in your repository to enable automated execution of Page Load Time (PLT) tests via the CI/CD workflow.

Procedure:

1.  Obtain the two predefined YAML files using the link provided below. These files contain the complete logic and configuration required to automate Page Load Time (PLT) testing through the CI/CD pipeline.
**Link:**

2.  Create a dedicated feature branch from your main or working branch within the repository.

3.  Add the following files to the root directory of the new branch:

    - **PipelineCollection.yml-** This is the reusable pipeline template that defines the core logic shared across executions.
      > *Do not modify this file unless explicitly required.*

    - **execution-pipeline.yml-** This is the main execution file that references the template and contains configurable parameters such as baseURL, tenantId, and test details, which should be tailored to your specific use case.
      > *You only need to update the parameters according to your setup. The structure of the file should remain unchanged.*

***Note:** Ensure that the template: path in the YAML file accurately references the relative location of PipelineCollection.yml.*

**Parameters Description:**

- **Base URL**: Endpoint of the backend API that initiates test collections and PLT evaluation.

- **Tenant ID**: Identifier for the Azure AD tenant handling authentication.

- **Wait Time**: Delay (in minutes) before checking Test Run execution status. To ensure that all executions have sufficient time to complete, calculate the wait time using the total number of pages in the report and the total load count.

  **Total Load Count** = Page 1 Load Count + Page 2 Load Count + ... + Page N Load Count

  **Calculate Wait Time:** 
Wait Time (minutes) = Total Load Count × 0.1
Example:
    - Page 1 Load Count: 6
    - Page 2 Load Count: 9
    - Page 3 Load Count: 5
    - Total Load Count: 6 + 9 + 5 = 20
    - Wait Time: 20 × 0.1 = 2 minutes

  <br>
  Quick Reference Table:

  | Total Load Count   | Wait Time (minutes)                        |
  |--------------------|--------------------------------------------|
  | 10                 | 1                                          |
  | 25                 | 3                                        |
  | 50                 | 5                                          |
  | 100                | 10                                         |
  | 500                | 50                                         |

- **Key Vault Group**: Reference to the configured variable group.

- **Test Details**: JSON structure defining test configuration.
  **Structure:**

    **testRuns:** An array of objects where each object should include the following fields:

    - **workspaceId** -- The unique identifier of the Power BI workspace containing the report

    - **reportId** -- The unique identifier of the Power BI report to be tested.

    - **pageId** -- The unique identifier of the specific page within the report.
    
       ***Note:** If the pageId is incorrect or not found, the PLT (Page Load Time) of the report's default page will be returned.*

    - **reportName** -- The name of the Power BI report

    - **pageName** -- The name of the page to be tested.

    - **workspaceName** -- The name of the workspace.

    - **loadTestingCount** -- The number of users for the page to be load tested.

    - **isRLS** - Indicates whether the report is configured with Row-Level Security (RLS). Use true for RLS-enabled reports and 0 otherwise.

    &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;***Note:** The following fields are required **only when isRLS is set to true (RLS-enabled reports)***
  - **roleName** -- Specifies the name of the RLS role to be applied.

  - **roleEmailId** -- Email address of the user associated with the specified role.

  - **datasetId** -- The unique identifier of the Power BI semantic model associated with the report being tested.

- **createdBy:** User email creating the Pipeline Collection Test

- **testRunName:** Name of Test Collection.

***Note:** The report or page to be tested must reside within a workspace that contains its associated semantic model. Additionally, the Service Principal (SPN) must have at least Member access to that workspace in order to retrieve the report and perform the PLT (Page Load Time) calculation.*

**Step 4: Trigger the Pipeline Execution**

This step involves manually initiating the configured pipeline within Azure DevOps to validate inputs and perform load testing based on the defined parameters.

1.  Navigate to **Pipelines** in your Azure DevOps project.

2.  Select **New Pipeline**.

3.  Choose the appropriate repository and select the execution-pipeline.yml file from your feature branch.

4.  Click **Run** to start the pipeline execution.

  ***Note:** During the first execution, Azure DevOps may prompt for permission to allow the pipeline to access the Azure Key Vault using the configured service connection.*

  Once the pipeline starts, the following results can be observed:

<figure><img src="../.gitbook/assets/Picture17.png" alt="Pipeline Results"><figcaption></figcaption></figure>
<figure><img src="../.gitbook/assets/Picture18.png" alt="Pipeline Results"><figcaption></figcaption></figure>

**Understanding Pipeline Output**

Once the CI/CD pipeline is triggered, it executes two key stages: **Create Test Run** and **Generate Test Report**. Each stage provides valuable feedback directly within the Azure DevOps pipeline logs. Below is a summary of what you can expect and how to interpret the results.

**✅ Create Test Run**

This stage handles the setup and execution of the test run. Key outputs include:

- **OAuth token generation**.

- **Test run creation**, where a unique TestRunID is generated.

- **Load validation**, which checks if the current load is within the cluster capacity.

- **Execution confirmation**, indicating successful test initiation.

This confirms that the backend system has accepted and scheduled the test.

**📄 Generate Test Report**

After the test run is completed, this stage fetches and displays the results in a structured format. For each tested page/report, it shows:
- **Collection Name:** Name of the tested collection.
- **Page level details:** 

  - **Page Name**: The name of the specific report page tested.

  - **Load Testing Count:** Number of times the page was loaded simultaneously during the test.

  - **Status**: Result of the test for the page — Passed, Failed, In Progress, or Not Started.

  - **Load Time**: The average time (in seconds) it took to load the page.

  - **90th Percentile Load Time**: Time within which 90% of the loads for the page were completed.

  - **Executed At**: Timestamp when the test for the page was completed.

At the end of the report, a **summary** is provided:

- **Total Pages Tested:** Number of total pages tested

- **Total Load Testing Count:** Combined load count across all pages

- **Average Load Time:** Average of load times across all pages

- **90th Percentile Time:** Average of 90th percentile times across all pages

- **Pass/Fail Count:** Total number of pages that passed or failed

***Note:** If you wish to view detailed test results or check the status of a test run that is still in progress (even after the configured wait time has elapsed), you can do so through the **Insight Report** available on the LoadFAST portal.*

To access it:

1.  Open the **LoadFAST portal**.

2.  Navigate to the **Insight Report** from the left-hand menu.

3.  In the filters, select **External** under Source Type.

<figure><img src="../.gitbook/assets/Picture22.png" alt="Insight Report Filter"><figcaption></figcaption></figure>

4.  **Copy the collection name** from the Pipeline run logs. 

<figure><img src="../.gitbook/assets/Picture20.png" alt="Pipeline Run Logs"><figcaption></figcaption></figure>

5.	Use this collection name to **filter** the Insight Report and view execution details.

<figure><img src="../.gitbook/assets/Picture21.png" alt="Insight Report Execution Details"><figcaption></figcaption></figure>