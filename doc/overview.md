# Lift & Shift DC Migration Overview

#### [prev](./welcome.md) | [home](./welcome.md)  | [next](./scan.md)

## [**Scan Milestone**](./scan.md)
During this phase discovery tooling is ran in the migratable state. 

## [**Assess & Select Migration Waves Milestone**](./assess.md) 
During this phase, typically lengthy, the scan results are reviewed to decide on lift and shift readiness and understand dependencies which will help build the migration waves.

## [**Design and Build the Landing Zone Milestone**](./landingzone.md) 
During this phase, typically lenghty, a design document for the Landing Zone (networking, governance, and operations) is developed and signed off. Build of the landing zone is 
performed based on this design.

>**Note**: The Assess & Select Workload milestone and the Design and Build the Landing Zone milestone can optionally be ran in parallel. 

## Replication of Migration Waves Milestone

### [**Replication of Migration Waves Milestone**](./replication.md) 
During this phase, a subnet of migration waves identified will be enabled for replication using a phased approach to adapt to current available bandwidth and ensure healthy replication.

### [**[Coming Soon] Redeployment of Migration Waves Milestone**](.\devops-iac-redeployment.md)
During this phase, we will be taking the approach of using the Azure Migrate Assessment findings in order to set up an Azure DevOps Pipeline with the appropriate tasks needed for VM Redeployment/Rehosting.

## End to End Test Migration Wave Milestone 

### [**End to End Test Migration Wave Milestone**](./testing.md) 
During this phase, typically missed but important, each migration wave identified during the Assess & Select Workload milestone is tested in Azure prior to the final cutover. Various test cases will be discussed during the presentation.

### [**[Coming Soon] Redeploy: Testing Environment for Migration Waves Milestone**](.\devops-iac-testing.md)
During this phase, we will explore using an isolated or production VNet in order to redeploy a subset of the defined migration wave to test the server functionality with the parameters from the Azure Migrate Assessment. This also includes recommendations for incorporating test cases into your Azure DevOps pipeline.

## Waves Migration & Post Go-Live Milestone

### [**Waves Migration & Post Go-Live Milestone**](./migration.md) 
During this phase, each migration wave is cutover to Azure and validated for expected functionality. For Post Go-live, each migration wave is handed over to Azure operations teams for the defined soak period. 

### [**[Coming Soon] Redeploy: Wave Migration & Post Go-Live Milestone**](.\devops-iac-migration.md)
During this phase, the sample pipeline for migration waves are configured with parameters that match your current migration wave. For Post Go-Live, some automation recommendations are explored to validate your migration wave environment.

![Concept Diagram](https://github.com/Azure/fta-liftandshift-dcmigration/blob/main/png/LiftandShift-dcmigration-workflow.PNG)

