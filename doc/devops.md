# DevOps/IaC Guidance for Migrations
## Redeployment/Rehosting of Migration Waves 
This section outlines the steps needed in order to execute an Azure DevOps Pipeline with the appropriate tasks needed for VM Redeployment/Rehosting.
 
### Redeployment/Rehosting Pre-Requisites 
* Prepared list of servers to be migrated delineated by migration wave
* Set up variables/parameters for the VM templates that include:
    * Sizing Information
    * Amount of Disks
    * Storage
    * Marketplace Image
        * OS
        * needs to be identified and include any prebaked software needed for the migration
    * Tags
    * Target virtual network and subnet
    * Target subscription and resource group
    * Optional
        * Tags
        * Redundancy (AV Set or Availability Zones)
* Naming conventions for resources in migration waves/environments
    * [Guidance](https://docs.microsoft.com/en-us/azure/cloud-adoption-framework/ready/azure-best-practices/resource-naming)
    * [Abbreviations Per Resource](https://docs.microsoft.com/en-us/azure/cloud-adoption-framework/ready/azure-best-practices/resource-abbreviations)
 
### Redeployment/Rehosting Tools
 
#### Bicep
Bicep is a declarative language that deploys Azure resources. In this migration scenario, it is useful for standardizing the type of VMs, Virtual Networks, Resource Groups, etc. that are being migrated to Azure.
 
Below is guidance for getting started with creating Bicep templates and integrating it within Azure DevOps Pipelines: 
* [Bicep CLI commands and overview](https://docs.microsoft.com/en-us/azure/azure-resource-manager/bicep/bicep-cli)
* [Integration with Azure DevOps Pipelines](https://docs.microsoft.com/en-us/azure/azure-resource-manager/bicep/add-template-to-azure-pipelines)
    * Uses Azure CLI Task to execute the Bicep deployment
* [Pre-deployment checks with Bicep](https://docs.microsoft.com/en-us/azure/azure-resource-manager/bicep/deploy-what-if?tabs=azure-powershell)
 
#### Shared Image Gallery + Azure Image Builder
* Shared Image Gallery can be utilized to manage, share, and globally distribute VM images within Azure. In the context of Migrations, it can be used for storing images utilized for the deployment.
    * [Shared Image Gallery Documentation](https://docs.microsoft.com/en-us/azure/virtual-machines/shared-image-galleries)
* Azure Image Builder is used to templatize VM Image customizations in a declarative way. In the context of migrations, it can be used in conjunction with Shared Image Gallery to execute custom pre- and post- scripts and install extensions onto the migrated VMs.
    * [Azure Image Builder Documentation](https://docs.microsoft.com/en-us/azure/virtual-machines/image-builder-overview)
    * [DevOps Task for Azure Image Builder](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/image-builder-devops-task)

#### Azure DevOps
* Azure DevOps Pipelines are used to automate and build code projects.
    * [Using Azure Pipelines](https://docs.microsoft.com/en-us/azure/devops/pipelines/get-started/pipelines-get-started?view=azure-devops)
    * [Catalog of the built-in tasks for build-release and Azure Pipelines](https://docs.microsoft.com/en-us/azure/devops/pipelines/tasks/?view=azure-devops) 
* Azure DevOps Repos is a version control tool that can be utilized to store files. In the context of migrations, it can be used to store YAML files such as the variables.yml and pipeline.yml for the automated workflow and accompanying test scripts for executing the deployment of servers.
    * [Azure Repos Documentation](https://docs.microsoft.com/en-us/azure/devops/repos/get-started/?view=azure-devops)
* Requirements for Migration
    * Azure DevOps Project
        * Permissions for utilizing Pipelines and Repos
        * Personal Access Token
    * Service Principal connected to Azure AD in your tenant (used to create a service connection in Azure DevOps)
    * Powershell Module (`Az`) installed
        * [Using the Powershell DevOps Task](https://docs.microsoft.com/en-us/azure/devops/pipelines/tasks/utility/powershell?view=azure-devops)
            * This task runs the scripts in order of execution with the appropriate variables.
        
#### 3rd Party Orchestration Engines
The rehost/redeployment of migrated servers can also be executed with automation using the following options below:
* GitHub Actions
    * GitHub Actions can be used as a CI/CD pipeline to automate the migration of VMs. Code from GitHub can be utilized for these deployments.
    * [GitHub Actions Documentation](https://docs.github.com/en/actions)
* Jenkins with Ansible
    * Jenkins can be utilized to orchestrate the flow of migration waves and VMs that are being provisioned with Ansible Infrastructure as Code templates.
    * [Jenkins User Documentation](https://www.jenkins.io/doc/)
    * [Ansible Documentation](https://docs.ansible.com/ansible/latest/index.html)

 
### Pipeline Execution for Rehost/Redeployment
* Set up variables needed for the CI/CD pipeline in a variables.yml file based on the environment
* Example Pipeline Stages for Redeployment/Rehosting of Migration Waves
    * Initialize Redeployment of Servers
* Validate the Migration Pre-requisites
* Initialize the Redeployment utilizing input parameters (CSV, variables.yml)
    * Dry Run
* Ensure that all the appropriate constructs are in the environment
    * Start Deployment of Servers
    * Validation of Environment 

## Testing
 
### Pre-Requisites 
* Outline parameters that simulate a smaller scale version of your environment
* Setup Bicep Scripts to be utilized with smaller testing environment 
    * Set up an isolated VNet and test if there is the correct connectivity
* Use appropriate Powershell Scripts that correlate to the types of tests needed for your deployment:
    * Smoke Test
    * UAT
    * Failover 
 
### Pipeline Execution for Testing
* Example Pipeline Stages for Test Migration
    * Initialize Test Migration
* Outline input parameters
* Run initial script with Bicep template
    * Start Test Migration
    * Clean Up Test Migration
* Delete testing resources from environment 
    * Initialize Test Migration
* Outline input parameters
    * Start Test Failover
    * Clean up Test Failover

### Recommendations for Testing Phase
* Block a maintenance window when executing the CI/CD Pipeline


 
## Migration
 
### Pre-Migration Activities
*  Delineate CI/CD pipeline based on environment
    * Ensure have the appropriate bicep files with the correct parameters
    * Migrate via the pipeline for environments in the order of non-prod to prod

### Pipeline Execution for Migration
* Example Pipeline Stages for Migration
    * Initialize Migration
        * Declare input parameters
    * Start Migration
        * Migrate via IaC in specified waves (non-prod to prod as recommended path)

### Recommendations for Migration Phase 
* Post migration activities (Optional)
    * Validate connections to the VMs that were done in the Testing Phase now that the cutover is complete
    * BCDR Considerations 
        * Backup of Servers
            * Can be executed via Azure Policy with Azure Backup: 
                * [DevOps Task](https://docs.microsoft.com/en-us/azure/devops/pipelines/tasks/deploy/azure-policy?view=azure-devops) 
                * [Policy](https://docs.microsoft.com/en-us/azure/backup/backup-azure-auto-enable-backup#policy-4---preview-configure-backup-on-vms-with-a-given-tag-to-a-new-recovery-services-vault-with-a-default-policy)
        * Enable Azure Site Recovery for Disaster Recovery
            * [Tutorial to set up Azure VM disaster recovery with Azure Site Recovery](https://docs.microsoft.com/en-us/azure/site-recovery/azure-to-azure-tutorial-enable-replication)
    * Deploy Azure Disk Encryption to help secure disks and keep data safe from theft and unauthorized access
    * Maintenance of Shared Image Gallery with Azure DevOps for the releases of New Images/Image Versions
    * Monitoring of Cloud Assets Through Azure Monitor
        * [Workbooks](https://docs.microsoft.com/en-us/azure/azure-monitor/visualize/workbooks-data-sources)
            * [Library of Application Insights Workbooks](https://github.com/microsoft/Application-Insights-Workbooks/tree/master/Workbooks) 
