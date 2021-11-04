# Milestone: Testing Environment for Migration Wave

#### [prev](./devops-iac-redeployment.md) | [home](./welcome.md)  | [next](./devops-iac-migration.md)

## Testing
 
## 1 Pre-Requisites
[Reference for Pre-Migration and Post-Migration Activities](https://github.com/Azure/fta-liftandshift-dcmigration/blob/main/doc/testing.md#12-technical)

### 1.1\. Pre-Migration Tasks 
- Setting up test pipeline by defining parameters for isolated VNet (i.e. CIDR block, NSG Ports will open on the test subnet, etc.)
- Set Migration order after testing in an isolated VNet from non-prod to prod workloads


### 1.2\. Post-Migration Tasks 
- Validate VM migration was successful and that applications are functioning as should be

### 1.3\. Create IaC templates that outline a smaller scale environment 
- Set up an isolated VNet to test if there is the correct connectivity ([Guidance for identifying target VNet](https://github.com/Azure/fta-liftandshift-dcmigration/blob/main/doc/testing.md#23-identify-target-vnets-tests-and-migration-workflow))
- If unable to set up an isolated VNet for testing, set up a prod VNet in parallel with the parameters needed for production workloads to move to Azure. Perform tests on a small subset of those workloads (non-prod first)

### 1.4\. Create the appropriate Powershell Scripts that correlate to the [types of tests](https://github.com/Azure/fta-liftandshift-dcmigration/blob/main/doc/testing.md#2-migration-plan-definition) needed for your deployment:
- Smoke Test
- UAT
- Failover 

## 2 Pipeline Execution for Testing

### 2.1\. Outline parameters that simulate a smaller scale version of your environment (use [`variables.yml`](<link-here>) as a sample)

### 2.2\. Create a `testing-pipeline.yml` for resource execution using the [template](<link to template>) as a baseline
Pipeline Tasks:
- Outline input parameters
- Start Test Migration
    - Create VNet, Compute and Storage Resources
- Run Testing Scripts
    - Smoke Test
    - UAT
    - Failover 
- Validate Test Environment
- Clean up Test Resources 

### 2.3\. Perform a dry run on the `testing-pipeline.yml` (<link here>) on your environment to validate the correct parameters will be executed 

### 2.4\. Execute the isolated VNet Testing Pipeline

### 2.5\. (Optional) For the utilizing the final Migration VNet


## 3 Recommendations for Testing Phase
- Consider inputing error handling and adding a task for your rollback plan within your pipeline


 