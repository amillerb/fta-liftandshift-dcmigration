## How to import the template into Azure DevOps

### Pre-requisites:

[Create a DevOps Organizaton](https://docs.microsoft.com/en-us/azure/devops/organizations/accounts/create-organization?view=azure-devops#create-an-organization) or use an existing one. 

### Process:

1. Navigate to the [Azure DevOps Demo Generator](https://azuredevopsdemogenerator.azurewebsites.net/Account/Verify) and sign into your DevOps organization.
2. Fill in **Project Name**, select your Organization, and select **Choose Template**.
3. Select **Private** and upload [this zip file](/artifacts/migration-iac.zip).
4. Select **Create Project** on the main page. 
5. After the successfully provisioning of the template, go to the Project > Boards > Backlogs and on the top-right click on the engine (Configure team settings) and select Waves, Deliverables, Activities then click on "Save and close".

![backlog-setting-1](/png/backlog-setting-1.png)

6. Now change to view the Waves then you you have all set, containing all Waves, Deliverables and Activities.

![backlog-setting-2](/png/backlog-setting-2.png)
