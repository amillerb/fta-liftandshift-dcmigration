## How to import the template into Azure DevOps

### Pre-requisites:

[Create a DevOps Organizaton](https://docs.microsoft.com/en-us/azure/devops/organizations/accounts/create-organization?view=azure-devops#create-an-organization) or use an existing one. 

### Process:

1. Navigate to the [Azure DevOps Demo Generator](https://azuredevopsdemogenerator.azurewebsites.net/Account/Verify) and sign into your DevOps organization.
2. Fill in **Project Name**, select your Organization, and select **Choose Template**.
3. Select **Private** and upload [this zip file](/artifacts/iac-migration.zip).
4. Select **Create Project** on the main page. 
5. After the successfully provisioning of the template, go to the Project > Boards > Backlogs and on the top-right click on the engine (Configure team settings) and select Epics, and Stories then click on "Save and close".

![backlog-setting-0](/png/backlog-setting-0.png)


![backlog-setting-1](/png/backlog-setting-1.png)

6. Now change to view the Epics then you have all set, containing all Epics, User Stories and Tasks.

![backlog-setting-2](/png/backlog-setting-2.png)

### Customization:

Here is a guidance over the process customization to have something different than Epics, Stories and Taks. In this case we'll have Waves, Deliverables and Activitites:

1. Click on the Azure DevOps logo in the top 
2. Click Click on Organization Settings
3. Go to Boards > Process
4. Right click on Agile then click to Create inherited process
5. Name as you want. In this case let's name as Migration, then click to Create process
6. Click on the Process created (Migration in this case)
7. On Work item types, click to **+ New work item type** and let's as below. Please note that you can customer the icon and the color for each one. After you click to create, a new window will be expanded to set extra details as Layout, States and Rules. You don't need change nothing here, just return to previous screen and continue the creation.
7.1 Wave
7.2 Deliverable
7.3 Activity
8. On All Process > Migration, click to Backlog levels and then click to **+ New top level portfolio backlog**
9. For each case, create a name and assotiate with the work item types on the backlog level. Example:

![portfolio-backlog-1](/png/portfolio-backlog-1.png)
![portfolio-backlog-2](/png/portfolio-backlog-2.png)
![portfolio-backlog-3](/png/portfolio-backlog-3.png)

10. Then you'll have something like this:

![portfolio-backlog-4](/png/portfolio-backlog-4.png)

