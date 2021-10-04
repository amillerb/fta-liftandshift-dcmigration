## How to import the template into Azure DevOps

### Pre-requisites:

[Create a DevOps Organizaton](https://docs.microsoft.com/en-us/azure/devops/organizations/accounts/create-organization?view=azure-devops#create-an-organization) or use an existing one. 

### Process:

1. Navigate to the [Azure DevOps Demo Generator](https://azuredevopsdemogenerator.azurewebsites.net/Account/Verify) and sign into your DevOps organization.
2. Go to https://aka.ms/fta/iacmigrationtemplate, sign into your DevOps organization and you already will be in the correct template selection for IaC Migration (Please note that if you click on Choose template, this template is available under **FastTrack for Azure** tab as well)
3. Select **Create Project** on the main page. 
4. After the successfully provisioning of the template, go to the Project > Boards > Backlogs and on the top-right click on the engine (Configure team settings). Validate that Epics and Stories are selected and then click **Save and Close**. 

![backlog-setting-0](/png/backlog-setting-0.png)


![backlog-setting-1](/png/backlog-setting-1.png)

5. Now change to view the Epics then you have all set, containing all Epics, User Stories and Tasks.

![backlog-setting-2](/png/backlog-setting-2.png)

### Customization:

It is recommended to utilize Wave, Deliverable, and Activity terminology in naming the work items, so here is a guidance over the process of customization to have something different than Epics, Stories and Tasks:

1. Click on the Azure DevOps logo in the top 
2. Click on Organization Settings
3. Go to Boards > Process
4. Right click on Agile then click to Create inherited process
5. Name as you want. In this case let's name as Migration, then click to Create process
6. Click on the Process created (Migration in this case)
7. On Work item types, click to **+ New work item type** and let's create three: Wave, Deliverable, and Activity.  Please note that you can customize the icon and the color for each one. After you click to create, a new window will be expanded to set extra details as Layout, States and Rules. You don't need change nothing here, just return to previous screen and continue the creation.
8. On All Process > Migration, click to Backlog levels and then click to **+ New top level portfolio backlog**
9. For each case, create a name and associate with the work item types on the backlog level. Example:

![portfolio-backlog-1](/png/portfolio-backlog-1.png)

![portfolio-backlog-2](/png/portfolio-backlog-2.png)

![portfolio-backlog-3](/png/portfolio-backlog-3.png)

10. Then you'll have something like this:

![portfolio-backlog-4](/png/portfolio-backlog-4.png)

11. Under Organization Settings, go to Boards > Process. Click on the process where initially our project was configured, Agile in this case.
12. On the top, click to Projects, select your project and click to Change process:

![change-process](/png/change-process.png)

13. Then select the new process created, Migration in this case, and save:

![change-process-1](/png/change-process-1.png)

14. Go to the project > Boards > Backlogs and change the type of each item properly:

![change-type](/png/change-type.png)

15. After change the type of all items, remember to change the backlog settings to show the new types created. Under the Project > Boards > Backlogs and on the top-right click on the engine (Configure team settings) and select the new categories (Wave, Deliverable, and Activity) are selected and then click **Save and Close**.

![backlog-setting-0](/png/backlog-setting-0.png)

![backlog-setting-3](/png/backlog-setting-3.png)

16. Now you'll have something similar to this:

![backlog](/png/backlog.png)

