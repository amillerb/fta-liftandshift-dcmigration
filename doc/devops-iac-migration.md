# Milestone: Wave Migration and Post Migration Activities

#### [prev](./devops-iac-testing.md) | [home](./welcome.md)  

## Overview

This section outlines the recommended migration steps to execute an Azure DevOps Pipeline for the deployment of servers. This is a sample pipeline deployment that can be customized to your Migration Wave cycles outlined in the exported Azure Migrate Assessments.

## 1 Pre-Requisites
Please refer to the [Milestone: Redeployment/Rehosting of Migration Waves](./devops-iac-redeployment.md) page in order to have the correct setup for this deployment.
* Reference Migration Tasks: [Milestone: Wave Migration and Post Go-Live](https://github.com/Azure/fta-liftandshift-dcmigration/blob/main/doc/migration.md)
> Note: The assessment CSV acts as the source of deployment information for the migration wave execution via the Azure Pipeline. Please ensure that once the CSVs are created that the unscoped VMs from the `All_Assessed_Machines.csv` and `All_Assessed_Disks.csv` files are manually omitted.

### 1.1\. Pipeline Stages for Migration utilizing the provided [template](../pipelines/rehost/migration-pipeline.yml).
- Setup Cutover Window within the pipeline
    - Ensure that there is a backup of the servers before cutover
- Initialize Migration
    - Declare input parameters and modify Target Subscription
- Start Migration
    - Migrate via pipeline specifications in migration waves
- Have rollback plan ready for execution if needed (send traffic to previous server)

## 2 Pipeline Execution for Rehost/Redeployment
This section covers utilizing Azure Pipelines to execute Powershell scripts to create the environment to rehost the VMs within the specified Azure environment.

> Note: Guidance for utilizing 3rd Party Orchestration Engines (Optional) can be found [here](https://github.com/Azure/fta-live-iac#other-orchestrators)

### 2.1\. Based on the migration wave, manually fill in variables needed for the CI/CD pipeline, using the [variables.yml](../pipelines/rehost/variables.yml) file as a template.

### 2.2\. Create a [migration-pipeline.yml](../pipelines/rehost/migration-pipeline.yml) for resource execution using the templates as a starter pipeline.

### 2.3\. Execute the pipeline for the appropriate migration wave and environment.

## 3 Post Go-Live 
### 3.1\. Post migration activities (Optional)
- Validate connections to the VMs that were done in the Testing Phase now that the cutover is complete
- BCDR Considerations 
    - Backup of Servers
        - Can be executed via Azure Policy with Azure Backup: 
            - [DevOps Task](https://docs.microsoft.com/en-us/azure/devops/pipelines/tasks/deploy/azure-policy?view=azure-devops) 
            - [Policy](https://docs.microsoft.com/en-us/azure/backup/backup-azure-auto-enable-backup#policy-4---preview-configure-backup-on-vms-with-a-given-tag-to-a-new-recovery-services-vault-with-a-default-policy)
    - Enable Azure Site Recovery for Disaster Recovery
        - [Tutorial to set up Azure VM disaster recovery with Azure Site Recovery](https://docs.microsoft.com/en-us/azure/site-recovery/azure-to-azure-tutorial-enable-replication)
- Deploy Azure Disk Encryption to help secure disks and keep data safe from theft and unauthorized access
- Maintenance of Shared Image Gallery with Azure DevOps for the releases of New Images/Image Versions
- Monitoring of Cloud Assets Through Azure Monitor
    - [Workbooks](https://docs.microsoft.com/en-us/azure/azure-monitor/visualize/workbooks-data-sources)
        - [Library of Application Insights Workbooks](https://github.com/microsoft/Application-Insights-Workbooks/tree/master/Workbooks)