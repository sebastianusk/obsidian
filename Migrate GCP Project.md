---
topic:
  - devops
---
In GCP, you have the concept of :
1. organization, it's like AWS Organization
2. project, it's like an AWS Account
to migrate you'll need:
- access as project mover at the project source
- access as project creator at the organization destination
- organization policy admin on both side, then:
	- set `constraints/resourcemanager.allowedExportDestinations` to be `under:organizations/{orgId}` at the organization source
	- set `constraints/resourcemanager.allowedImportSources` to be `under:organizations/{orgId}` at the organization destination
- then to run the command, you have to use cli `gcloud beta projects move {projectId} --organization {orgId}`

As for additional resources given by the GCP support:
  
1. [https://cloud.google.com/resource-manager/docs/create-migration-plan]https://cloud.google.com/resource-manager/docs/create-migration-plan
2. [https://cloud.google.com/resource-manager/docs/assign-iam-roles]https://cloud.google.com/resource-manager/docs/assign-iam-roles
3. [https://cloud.google.com/resource-manager/docs/configure-org-policy](https://cloud.google.com/resource-manager/docs/configure-org-policy)
4. [https://cloud.google.com/resource-manager/docs/handle-special-cases](https://cloud.google.com/resource-manager/docs/handle-special-cases)
5. [https://cloud.google.com/resource-manager/docs/perform-migration](https://cloud.google.com/resource-manager/docs/perform-migration)

