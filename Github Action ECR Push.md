---
topic:
  - devops
---
to explain on how the Github Action can run ECR push you'll need to understand [[DEVO0009-Oauth2]] and [[DEVO0010-AWS IAM Assume Role]] 
- checklist what needs to be done:
	- create Github OIDC provider
	- create IAM assumable role
	- run the github action while run the `configure-aws-credentials`