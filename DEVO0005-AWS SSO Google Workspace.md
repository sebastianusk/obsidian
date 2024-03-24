To integrate well with the AWS SSO Sync, we can use https://github.com/awslabs/ssosync. A bit of points on these:
- the grouping is only able to get a list of the roles with some specific queries: https://developers.google.com/admin-sdk/directory/v1/guides/search-groups
- you cannot half manage the AWS SSO, it will clean up the other groups that are not included there

components that need to be built using terraform:
1. Then you can use the terraform to define the SSO permission set: https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/ssoadmin_permission_set_inline_policy
2. pull out the groups using `data` where the group is created by SSOsync
3. assign the permission to the account and group

Option on the interface:
- one object declarative: build based on group -> account -> permission -> policy
- build separately:
	- create permission -> policy
	- assign permission to group & account
