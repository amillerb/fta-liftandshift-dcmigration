# Milestone: Redeployment/Rehosting of Migration Waves

#### [prev](./devops-iac-redeployment.md) | [home](./welcome.md)  | [next](./devops-iac-testing.md)
 
This section outlines the steps needed in order to execute an Azure DevOps Pipeline with the appropriate tasks needed for VM Redeployment/Rehosting.

[Infrastructure as Code Guidance](https://github.com/Azure/fta-live-iac#what-is-infrastructure-as-code)

## 1 Pre-Requisites
### 1.1\. Gather VM information from the Migration Discovery (using CSV generated from the discovery as a reference) to setup a `variables.yml` for pipeline execution.

## 2 Redeployment/Rehosting Tools - Planning and Implementation
### 2.1\. Create a project in Azure DevOps using guidance from the [DevOps/IaC Template](.\importing-template.md). This project template gives a baseline for getting started with planning and tracking tasks using [Azure Boards](https://docs.microsoft.com/en-us/azure/devops/boards/get-started/?view=azure-devops) and executing this migration path with [Azure Repos](https://docs.microsoft.com/en-us/azure/devops/repos/get-started/?view=azure-devops) and [Azure Pipelines](https://docs.microsoft.com/en-us/azure/devops/pipelines/get-started/pipelines-get-started?view=azure-devops). 

### 2.2\. Within the project, create the appropriate repo for template storage and version control.

Recommended folder structure:
![Migration Tree](../png/migration-repo-structure.png)

- `bicep-modules`:  folder to keep bicep files in for reference
- `scripts`: folder to keep powershell files for executing different test and validation scripts
- `testing-pipeline.yml`: file for testing in an isolated VNet
- `migration-pipeline.yml`: file for running non-prod and prod migration waves


### 2.3\. Create IaC templates that correlate to your deployment
If utilizing Bicep for your deployment, start [here](https://github.com/Azure/fta-live-iac#bicep) for a list of resources relating to getting started with Bicep and integrating it into an Azure DevOps Pipeline.

- Set up any components such as a Shared Image Gallery with custom images
    - [Shared Image Gallery Documentation](https://docs.microsoft.com/en-us/azure/virtual-machines/shared-image-galleries)
    - [Azure Image Builder Documentation](https://docs.microsoft.com/en-us/azure/virtual-machines/image-builder-overview)
    - [DevOps Task for Azure Image Builder](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/image-builder-devops-task)
-  Create compute, network and storage templates for execution


## 3 Pipeline Execution for Rehost/Redeployment
This section covers utilizing Azure Pipelines to executer IaC templates. The recommendation is to separate the pipelines based on environment (test, non-prod and prod pipelines)

> Note: Guidance for utilizing 3rd Party Orchestration Engines (Optional) can be found [here](https://github.com/Azure/fta-live-iac#other-orchestrators)

### 3.1\. Based on the migration wave (i.e. non-prod), outline variables needed for the CI/CD pipeline in a [variables.yml](<link-to-page>) file.

### 3.2\. Create a pipeline.yml for resource execution using the [template](<link to template>) as a baseline
Pipeline Components: 
- Test Pipeline
    - Testing scripts
    - Isolated VNet to test and validate VMs in
- Non-Prod
    -  Non-Production Migration Wave Workload
- Prod
    - Production Migration Wave Workload

### 3.3\. Perform a dry run of the pipeline ensure that all the right parameters are in place for the non-prod environment

### 3.4\. Execute the pipeline for the migration wave 

