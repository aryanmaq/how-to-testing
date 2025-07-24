

# LoadFAST FAQ's


## Subscription Plans

**What plans are available for LoadFAST?**
- **Free Plan:** Perform load test up to 50 users ($0 + Azure infra cost) user not have to 
- **Pro Plan:** No limit on number of users ($1500/month + Azure infra cost)
*Note: Free support and upgrades are available in both the plans.*

**Where can I purchase LoadFAST?**
You can purchase LoadFAST from the [Microsoft Azure Marketplace](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/maqsoftware.powerbiloadanalyzer?tab=PlansAndPrice).

**How will I be billed for my subscription?**
Your subscription charges will appear on your monthly Azure invoice.

**Can I change my plan after purchase?**
Yes, you can upgrade or downgrade your plan at any time through the Azure portal.


## Set Up Details

**How do I set up and configure LoadFAST?**
- Step-by-step setup instructions are available in the documentation: [LoadFAST: Technical Documentation](https://maqsoftware.gitbook.io/loadfast-technical-documentation)
- For a quick overview, watch the [Demo video](https://links.maqsoftware.com/LoadFAST-demo)



## Key Features & Capabilities

**What are the key features and advantages of LoadFAST?**
- Supports load testing across a collection of reports with distributed user loads (concurrent users per report)
- Simulates realistic user interactions and applies Row-Level Security (RLS) during tests
- Enables concurrent load testing for up to **N users**, ensuring performance under real-world usage patterns
- Load tests are executed without caching, providing accurate performance metrics
- Detailed Insights & Reporting:
  - Identifies the **most expensive visuals** in a report
  - Measures **page load time** at report, page, and visual levels
  - Provides **user-level analytics** over time for granular performance insights
- Correlates test results with Microsoft Fabric capacity metrics for better resource planning


## GIT Integration Feature

**How does LoadFAST integrate with GIT and CI/CD pipelines?**

GIT integration allows you to perform load testing via pipeline automation, enabling CI/CD workflows for load testing scenarios.



## Data Privacy & Security

**How does LoadFAST handle data privacy and security?**
- LoadFAST does not store your report data. Only performance metrics and test configurations are retained for analysis.
- User authentication and access are managed via secure Azure AD integration.



## Potential Failure Scenarios

**What are some possible reasons for failure when using LoadFAST?**
- Insufficient Azure resources or permissions
- Incorrect RLS configuration
- Network connectivity issues
- Cluster not started or unavailable
- Exceeding user limits on Free Plan



## Troubleshooting & Frequently Encountered Issues

### Common Issues and Solutions

**Why is the page not loading?**
Clear cache and refresh.

**What should I do if I see 'Something Went Wrong'?**
Contact support.

---

### Create Collection

**Can we select a specific page while selecting a report?**
  - **Yes**, while selecting report dropdown arrow next to report name will open's all the pages you can untick the pages you dont need.  

**How do I apply a User Action?**
  - After selecting the report click dropdown next to report name then you will see **+** icon in user action column, you can add user action from there.

**Why is the User Action button disabled in an RLS-enabled report, and how can I apply a User Action?**  
  - If you've selected an **RLS-enabled report**, the **User Action** button will be disabled until you **configure RLS** details. Once RLS details is configured, you can click the dropdown arrow next to the report name to see the **+** icon and add a User Action.

**What should I enter in Role Name and Role Email while configuring RLS?**
   - In **Role Name**  select the specified role, in **Role Email ID** enter the email of the user having access to that report.

**What access levels can be assigned to collaborators?**
   - You can assign **Editor** or **Viewer** level access to the collaborator.

### Edit Collection

**Can I delete a collection?**
  - **No** , currently you can't delete a collection.

**Can I edit a collection?**
   - **Yes**, on collection you will see ![Edit Icon](attachment/edit-icon.png) click on it to edit the collection.

**Can i change Collaborators after creating collection?**
   - **Yes**, you can **add/removed** any collaborator.

**Can i change the Report after creating a collection?**
  - **Yes**, if you *havn't created test run* you can change the report.

### Main Page

**How can I find an old collection?**
  - Using **Search Bar** and **Filters** , you can easily find the collection.

**How can I see only the collections I created?** 
   - In **My Collection**, you will see the collection created by you.

**Can I see collections in both simple and detailed view?**
   - **Yes**, using **Table View** and **Tile View** you will be able to see both the detailed view and simple view of collections.

**How do I sign out?**
  - In **Header** top-right corner you will find User setting Icon click on it there you will see **Sign Out** Button.

### Create Test

**Why can't I switch 'Apply to all' / 'Percentage split' even after entering the user count?**
  - **Deselect** the current option before choosing another one.

**When should I use 'Apply to all' and when should I use 'Percentage split'?**
  - Use **Apply to all** when you want assign the specified load count to each page.
  - Use **Percentage split** when you want to divide the user count across report based on specified percentages.

**What does 'Total Load Testing Count' mean?**
   - It means the **total number of virtual machines** you want to simulate in the test run.

**What does 'Total Percentage Count: Effective' mean?**
   - It represents the **calculated distribution** of user load across clusters, based on the **percentage values** you’ve entered for each. it should be *100* to create test run.

**I clicked the Trigger button, but nothing happened. Why?**
   - If you see **triggered successfull** toast, then it  will *display result after some time*, just refresh the page using ![Refresh Icon](attachment/refresh.png) else check the cluster from admin settings.

**Why is the Trigger button disabled?**
   - Either you have only **Viewer** access or the  **Clusters** are Off, start the cluster from admin settings.

**What does 'Partially Passed' mean?**
  - It means *few pages* of report got **failed**.

### Admin Settings

**How can I check the status of a cluster?**
  - Go to **Admin Settings**, below select cluster you will find the status of cluster.

**How can I start or stop a cluster?**
   - Go to **Admin Settings > Cluster Management**, and select management type **Manual** and toggle **ON/OFF** button.

**Why isn't the cluster starting after selecting 'Auto'?**
   - In, **Auto** the cluster only get **Stopped** after specified hours, to start the cluster you have to **Manually** start the cluster.

**Can anyone start/stop the same cluster?**
  - **No**, only admin can start/stop the cluster.

### Insight Report

**Why is nothing visible in my Insight Report?**
Most probably you haven't selected the Collection or there is some issue in configuration.



## High Level Checklist

**Checklist for Users: Validate Before Implementing LoadFAST**

- [ ] Select a LoadFAST plan
- [ ] Purchase via Azure Marketplace
- [ ] Access setup docs and demo
- [ ] Check Azure/Power BI prerequisites
- [ ] Set up GIT integration (if needed)
- [ ] Review features
- [ ] Check privacy and security
- [ ] Know failure scenarios
- [ ] Test with sample reports
- [ ] Review common issues

---
