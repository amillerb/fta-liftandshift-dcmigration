# Milestone: Testing Environment for Migration Wave

#### [prev](./devops-iac-redeployment.md) | [home](./welcome.md)  | [next](./devops-iac-migration.md)

## Testing
 
## 1 Pre-Requisites
[Reference for Pre-Migration and Post-Migration Activities](https://github.com/Azure/fta-liftandshift-dcmigration/blob/main/doc/testing.md#12-technical)

### 1.1\. Pre-Migration Tasks 
- Setting up test pipeline by defining parameters for isolated VNet (i.e. CIDR block, NSG Ports that will open on the test subnet, etc.).
- Ensure that appropriate stakeholders are given the least privilege permissions to execute the pipelines.
- Define Migration approach through waves of execution
    - Understand dependencies to create migration waves/groups.
    - Define test cases.
    - Ensure Rollback plan is in place for the re-hosted VMs.
    - Make sure that test data is consistent with the data used in production.
- Clean up test resources that were deployed in an isolated VNet.

### 1.2\. Post-Migration Tasks 
- Validate VM migration was successful and that applications are functioning as should be
    - Perform capacity testing to ensure that functioning properly in production

### 1.3\. Create IaC templates that outline a smaller scale environment 
- Set up an isolated VNet to test if there is the correct connectivity ([Guidance for identifying target VNet](https://github.com/Azure/fta-liftandshift-dcmigration/blob/main/doc/testing.md#23-identify-target-vnets-tests-and-migration-workflow))
- If able to have a maintenance window to shut down on-prem workload for test migration, set up a prod VNet with the parameters needed for production workloads to move to Azure. Perform tests on a smaller VM waves of the workloads first.

### 1.4\. Create the appropriate Powershell Scripts that correlate to the [types of tests](https://github.com/Azure/fta-liftandshift-dcmigration/blob/main/doc/testing.md#2-migration-plan-definition) needed for your deployment:
- Smoke Test
- UAT
- Failover 

## 2 Pipeline Execution for Testing

### 2.1\. Outline parameters that simulate a smaller scale version of your environment (use [`testing-variables.yml`](../pipelines/testing-variables.yml) as a sample)

### 2.2\. Create a `testing-pipeline.yml` for resource execution using the provided [template](../pipelines/testing-pipeline.yml) as a baseline.
Pipeline Tasks:
- Outline input parameters
- Start Test Migration
    - Create VNet, Compute and Storage Resources
- Run Testing Scripts
    - Smoke Test
    - UAT
    - Failover 
- Validate Test Environment
- Delete Test Resources 

### 2.3\. Validate the correct parameters for the pipeline and execute the isolated VNet Testing Pipeline.

### 2.4\. If utilizing the final Migration VNet, set the maintenence window and prepare migration waves for execution using the sample pipeline [template](../pipelines/migration-pipeline.yml) for migration.
- If any of the tests fail within a pipeline stage, execute Rollback plan for the migration wave.