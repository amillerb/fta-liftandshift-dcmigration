# Milestone: Wave Migration and Post Migration Activities

#### [prev](./devops-iac-testing.md) | [home](./welcome.md)  

## 1 Pipeline Execution for Migration
### 1.1\. Example Pipeline Stages for Migration utilizing the provided [template](./pipelines/migration-pipeline.yml).
- Setup Cutover Window within the pipeline
    - Ensure that there is already a backup of the servers before cutover
- Initialize Migration
    - Declare input parameters and modify Target Subscription
- Start Migration
    - Migrate via IaC in specified waves (non-prod to prod as recommended path)
- Have rollback plan ready for execution if needed (send traffic to previous server)

## 2 Post Go-Live 
### 2.1\. Post migration activities (Optional)
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
