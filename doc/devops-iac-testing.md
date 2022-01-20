# Milestone: Testing Environment for Migration Wave

#### [prev](./devops-iac-redeployment.md) | [home](./welcome.md)  | [next](./devops-iac-migration.md)

This section outlines the steps needed in order to execute an Azure DevOps Pipeline with the appropriate tasks needed for setting up a test environment for migration. This implementation focuses on rehosting a subset of the defined migration wave in order to test the server functionality with the parameters from the Azure Migrate Assessment.

## 1 Pre-Requisites
To get started, the assumption is the following:
* The [discovery](https://github.com/Azure/fta-liftandshift-dcmigration/blob/main/doc/scan.md) is completed for the scoped VMs
* The [assessment](https://github.com/Azure/fta-liftandshift-dcmigration/blob/main/doc/assess.md) for the environment is created within Azure Migrate.
    * The assessment is the source for where the VMs in the pipeline are created. Please ensure that only the VMs that are scoped for the test environment are in the assessment. Please manually omit VMs not needed in the deployment.
* The assessment was exported as an Excel file to your local machine.
* An [Azure DevOps Organization](https://docs.microsoft.com/en-us/azure/devops/organizations/accounts/organization-management?view=azure-devops) is created and linked to your subscription in Azure.
* The [pipelines folder](../pipelines/) is cloned on your local machine.
* [Powershell](https://docs.microsoft.com/en-us/powershell/scripting/install/installing-powershell?view=powershell-7.2) and excel are installed on your local machine.


### 1.1\. Pre-Migration Tasks 
[Reference for Pre-Migration and Post-Migration Activities](https://github.com/Azure/fta-liftandshift-dcmigration/blob/main/doc/testing.md#12-technical)

- Define parameters needed for an isolated VNet implementation (i.e. CIDR block, NSG Ports that will open on the test subnet, etc.).
- Ensure that appropriate stakeholders are given the least privilege permissions to execute the pipelines.
- Define Migration approach through waves of execution
    - Understand dependencies to create migration waves/groups.
    - Define test cases.
    - Ensure Rollback plan is in place for the re-hosted VMs.
    - Make sure that test data is consistent with the data used in production.
- Clean up test resources that were deployed in an isolated VNet.

### 1.2\. Define parameters for your test environment
- Set up an isolated VNet to test if there is the correct connectivity ([Guidance for identifying target VNet](https://github.com/Azure/fta-liftandshift-dcmigration/blob/main/doc/testing.md#23-identify-target-vnets-tests-and-migration-workflow))
- If able to have a maintenance window to shut down on-prem workload for test migration, set up a VNet with the parameters needed for production workloads to move to Azure.
- Perform tests on a smaller VM waves of the workloads first.
- Choose non-prod VM Migration group to start the test functionality with.

### 1.3\. Create the appropriate scripts that correlate to the [types of tests](https://github.com/Azure/fta-liftandshift-dcmigration/blob/main/doc/testing.md#2-migration-plan-definition) needed for your deployment:
- Smoke Test
- UAT
- Failover

```
**[testing workflow diagram]**
```

## 2 Pipeline Execution for Testing

### 2.1\. Input parameters your environment using the [testing-variables.yml](../pipelines/testing/testing-variables.yml) as a template.

### 2.2\. Create a `testing-pipeline.yml` for resource execution using the provided [template](../pipelines/testing/testing-pipeline.yml) as a baseline. Below are a description of the tasks:
Pipeline Tasks:
- Outline input parameters
- Start Test Migration
    - Create isolated VNet (optional)
    - Within Powershell script:
        - Create the Migration Group Compute needed
- Validate Test Environment (manually or using test scripts)
    - Run Testing Scripts (if applicable)
        - Smoke Test
        - UAT
        - Failover
- Clean up Test Resources

### 2.4\. Validate Target VNet Tests
* If execute the isolated VNet Testing Pipeline, validate the pipeline has ran through the necessary tasks above.
* If utilizing the final Migration VNet, set the maintenance window and prepare migration waves for execution using the sample pipeline [template](../pipelines/testing/testing-pipeline.yml) for migration.
* If any of the tests fail within a pipeline stage, execute the Rollback plan for the migration wave.

### 2.5\. Post Test Migration Tasks 
- Validate VM migration was successful and that applications are functioning as should be
    - Perform capacity testing to ensure that functioning properly in production

### 2.6\. Expected Results 
* VNet created with specified parameters for testing its functionality before full migration of servers to Azure
* Standardized pipeline to utilize for deploying compute resources in Azure
* Pipeline provides option for executing tests within Azure on the testing resources that are deployed
* Pipeline performs clean up of test resources after validation of functionality