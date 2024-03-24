on AWS, we have IAM (Identity and Access Management). Generally, they provide access to AWS resources. There are a few components there:
1. IAM User:
	1. general user
	2. The user can create a token key (classic IAM token)
2. IAM Group
	1. collection of users
3. IAM Role
	1. role that anything can switch into after assuming assume role
	2. there is a trust entity to define what entity can assume
	3. can also use custom identity provider like GitHub
4. Policy
	1. rules that define what access that entity can hold
	2. defined using JSON file
5. IAM Identity Center
	1. previously called AWS SSO
	2. basically can provide better access management in the AWS Organization (cross-account)
	3. can also be the identity provider of anything else that support SAML