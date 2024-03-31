---
topic:
  - devops
---
1. Create a migration plan [1] - You should consider how your migration will impact the services running inside the project. Changes in the resource hierarchy caused by a project migration can lead to changes in inherited policies, such as organization policies and Identity and Access Management policies.
2. Assign Identity and Access Management roles [2] - You need a particular set of IAM roles to migrate a project between organization resources. You will also need permission to create and manage organization policies.You can get these permissions by acquiring the following roles:
	1. Project Mover (roles/resourcemanager.projectMover) on the project you want to migrate and its parent resource.
	2. Project Creator (roles/resourcemanager.projectCreator) on the destination folder or organization resource.
	3. Organization Policy Admin (roles/orgpolicy.policyAdmin) on both the source and destination organization resources.
3. Configure organization policies [3]
	1. To perform a project migration between organization resources, you must set the constraints/resourcemanager.allowedExportDestinations constraint, which defines the organization resources to which the project can be migrated.
	2. On the destination side, you must set the constraints/resourcemanager.allowedImportSources constraint that defines the organization resources from which projects can be imported.
	3. If either of these constraints are not properly set, the migration will fail with a FAILED_PRECONDITION error.
4. Address any special cases [4] - When you migrate a project between organization resources, there is a chance you'll need to address certain scenarios at the project and organization resource level. There can be services involved that you'd need to consider that As part of your migration plan, you should consider these cases if you depend on the services involved for the operation of your project
5. Perform the migration [5] - Once you have finished the above steps, you can use the Resource Manager API to migrate a project.