

# LoadFAST FAQ's


## Subscription Plans

**What plans are available for LoadFAST?**
- **Free Plan:** Perform load test up to 50 users ($0 + Azure infra cost).
   - With the Free Plan, platform fees are not charged; however, Azure infrastructure costs are borne by the user
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
<figure><img src="../.gitbook/assets/attachment/faq-collect-not-fetc.png" alt="Collection Not Fetched Toast"><figcaption></figcaption></figure>  


**What are the key features and advantages of LoadFAST?**
- Supports load testing across a collection of reports with distributed user loads (concurrent users per report)
<figure><img src="../.gitbook/assets/attachment/faq-max-load-count.png" alt="Load Count Exceeds Toast"><figcaption></figcaption></figure>  
- Enables concurrent load testing for up to **N users**, ensuring performance under real-world usage patterns
- Load tests are executed without caching, providing accurate performance metrics
  - Identifies the **most expensive visuals** in a report
  - Measures **page load time** at report, page, and visual levels
  - Provides **user-level analytics** over time for granular performance insights
<figure><img src="../.gitbook/assets/attachment/faq-rep-fail-user-action.png" alt="Report Failed during User Action"><figcaption></figcaption></figure>  


**How does LoadFAST automate load testing with CI/CD integration?**

<figure><img src="../.gitbook/assets/attachment/faq-trigger-off.png" alt="Trigger"><figcaption></figcaption></figure>  



- LoadFAST does not store your report data. Only performance metrics and test configurations are retained for analysis.


## Potential Failure Scenarios
<figure><img src="../.gitbook/assets/attachment/faq-Insight-not-loded.png" alt="Insight Report Loading Failed"><figcaption></figcaption></figure>  
**What are some possible reasons for failure when using LoadFAST?**

<figure><img src="../.gitbook/assets/attachment/faq-collect-not-fetc.png" alt="Collection Not Fetched Toast"><figcaption></figcaption></figure>  
*Recommended Actions:* 
- Refresh the page to reload the collections.  
<figure><img src="../.gitbook/assets/attachment/faq-cap-failed.png" alt="Capacity Report Loading Failed"><figcaption></figcaption></figure>  

**Load count exceeds cluster limit**  

- Navigate to Admin Settings and increase the load count as required.  
<figure><img src="../.gitbook/assets/attachment/edit-icon.png" alt="Edit Icon"><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/attachment/refresh.png" alt="Refresh Icon"><figcaption></figcaption></figure>
<figure><img src="../.gitbook/assets/attachment/faq-rep-fail-user-action.png" alt="Report Failed during User Action"><figcaption></figcaption></figure>  

*Recommended Actions:* 
- Confirm that embedding is enabled in the Power BI Admin Portal.  
- Ensure that tenant settings are configured correctly. For detailed instructions, refer to the [technical documentation](https://maqsoftware.gitbook.io/loadfast-technical-documentation/setting-up/prepare/pre-deployment/set-up-and-configure-the-power-bi-tenant-settings).


**Cluster is turned off when triggering a test**  
<figure><img src="../.gitbook/assets/attachment/faq-trigger-off.png" alt="Trigger"><figcaption></figcaption></figure>  

*Recommended Actions:* 
- Navigate to the **Admin Settings** page.  
<figure><img src="../.gitbook/assets/attachment/faq-go-to-setting.png" alt="Go to Admin Settings"><figcaption></figcaption></figure>  
- Under **Management Type**, select **Manual** if not already set.  
<figure><img src="../.gitbook/assets/attachment/Faq-manual-select.png" alt="Change Cluster Status"><figcaption></figcaption></figure>  
- Toggle the cluster status switch to **ON**.  
<figure><img src="../.gitbook/assets/attachment/Faq-toggle-on.png" alt="Toggle On"><figcaption></figcaption></figure>  
- Click **Apply** to activate the cluster.

**Insight Report fetch failed**  
<figure><img src="../.gitbook/assets/attachment/faq-Insight-not-loded.png" alt="Insight Report Loading Failed"><figcaption></figcaption></figure>  

*Recommended Actions:* 
- Review your configuration details in Admin Settings and update them if necessary.  
<figure><img src="../.gitbook/assets/attachment/faq-correct-insightdetail.png" alt="Update Insight Details"><figcaption></figcaption></figure>  
- Click **Apply** to save the changes.

**Insight Report not loading**  

*Recommended Actions:* 
- Verify that the report is configured correctly in [Power BI Services](https://app.powerbi.com/home).

**Capacity Report fetch failed**  
<figure><img src="../.gitbook/assets/attachment/faq-cap-failed.png" alt="Capacity Report Loading Failed"><figcaption></figcaption></figure>  

*Recommended Actions:* 
- Review your configuration details in Admin Settings and update them if necessary.  
<figure><img src="../.gitbook/assets/attachment/faq-capacity-detail-update.png" alt="Update Capacity Details"><figcaption></figcaption></figure>  
- Click **Apply** to save the changes.

**LoadFAST Web App not loading**  

*Recommended Actions:* 
- Confirm that the application is configured correctly. For guidance, refer to the [setup documentation](https://maqsoftware.gitbook.io/loadfast-technical-documentation/setting-up/configure/add-the-redirect-uris#navigate-to-the-redirect-uris-section-1).

**Admin Settings icon not visible**  

*Recommended Actions:* 
- Ensure that the App Role is created. For instructions, see the [documentation](https://maqsoftware.gitbook.io/loadfast-technical-documentation/setting-up/prepare/pre-deployment/create-an-app-registration-for-the-loadfast-api#create-an-app-role).  
- Assign the Admin Role as described [here](https://maqsoftware.gitbook.io/loadfast-technical-documentation/setting-up/configure/assign-admin-roles-in-the-application).


## Troubleshooting & Frequently Encountered Issues

### Common Issues and Solutions

**Why is the page not loading?**

Clear cache and refresh.

**What should I do if I see 'Something Went Wrong'?**

Contact support.

---

### Create Collection

**Can we select a specific page while selecting a report?**
  - **Yes**, while selecting a report, the dropdown arrow next to the report name will open all the pages. You can untick the pages you don't need.  

**How do I apply a User Action?**
  - After selecting the report, click the dropdown next to the report name. Then you will see the **+** icon in the user action column; you can add a user action from there.

**Why is the User Action button disabled in an RLS-enabled report, and how can I apply a User Action?**  
  - If you've selected an **RLS-enabled report**, the **User Action** button will be disabled until you **configure RLS** details. Once RLS details are configured, you can click the dropdown arrow next to the report name to see the **+** icon and add a User Action.

**What should I enter in Role Name and Role Email while configuring RLS?**
  - In **Role Name**, select the specified role. In **Role Email ID**, if you have admin permissions, enter the email of the user on whose behalf you want to view the report; otherwise, your own email will be auto-filled.

**What access levels can be assigned to collaborators?**
  - You can assign **Editor** or **Viewer** level access to the collaborator.

### Edit Collection

**Can I delete a collection?**
  - **No**, currently you can't delete a collection.

**Can I edit a collection?**
  - **Yes**, on the collection you will see <figure><img src="../.gitbook/assets/attachment/edit-icon.png" alt="Edit Icon"><figcaption></figcaption></figure>. Click on it to edit the collection.

**Can I change collaborators after creating a collection?**
  - **Yes**, you can **add/remove** any collaborator.

**Can I change the report after creating a collection?**
  - **Yes**, if you *haven't created a test run*, you can change the report.

### Main Page

**How can I find an old collection?**
  - Using **Search Bar** and **Filters**, you can easily find the collection.

**How can I see only the collections I created?** 
  - In **My Collection**, you will see the collections you created.

**Can I see collections in both simple and detailed view?**
  - **Yes**, using **Table View** and **Tile View**, you will be able to see both the detailed and simple views of collections.

**How do I sign out?**
  - In the **Header** at the top-right corner, you will find the User Settings icon. Click on it to see the **Sign Out** button.

### Create Test

**Why can't I switch 'Apply to all' / 'Percentage split' even after entering the user count?**
  - **Deselect** the current option before choosing another one.

**When should I use 'Apply to all' and when should I use 'Percentage split'?**
  - Use **Apply to all** when you want to assign the specified load count to each page.
  - Use **Percentage split** when you want to divide the user count across the report based on specified percentages.

**What does 'Total Load Testing Count' mean?**
  - It means the **total number of virtual machines** you want to simulate in the test run.

**What does 'Total Percentage Count: Effective' mean?**
  - It represents the **calculated distribution** of user load across clusters, based on the **percentage values** you’ve entered for each. It should be *100* to create a test run.

**I clicked the Trigger button, but nothing happened. Why?**
  - If you see a **triggered successful** toast, it will *display the result after some time*. Just refresh the page using <figure><img src="../.gitbook/assets/attachment/refresh.png" alt="Refresh Icon"><figcaption></figcaption></figure>; otherwise, check the cluster from admin settings.

**Why is the Trigger button disabled?**
  - Either you have only **Viewer** access or the **Clusters** are off; start the cluster from admin settings.

**What does 'Partially Passed' mean?**
  - It means *few pages* of the report **failed**.

### Admin Settings

**How can I check the status of a cluster?**
  - Go to **Admin Settings**. Below the selected cluster, you will find the status of the cluster.

**How can I start or stop a cluster?**
  - Go to **Admin Settings > Cluster Management**, select management type **Manual**, and toggle the **ON/OFF** button.

**Why isn't the cluster starting after selecting 'Auto'?**
  - In **Auto**, the cluster only gets **stopped** after the specified hours. To start the cluster, you have to **manually** start it.

**Can anyone start/stop the same cluster?**
  - **No**, only the admin can start/stop the cluster.

### Insight Report

**Why is nothing visible in my Insight Report?**
Most likely, you haven't selected the Collection or there is an issue in the configuration.



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
