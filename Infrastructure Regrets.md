---
topic:
  - devops
---
link: [https://cep.dev/posts/every-infrastructure-decision-i-endorse-or-regret-after-4-years-running-infrastructure-at-a-startup/](https://cep.dev/posts/every-infrastructure-decision-i-endorse-or-regret-after-4-years-running-infrastructure-at-a-startup/)

My main keytakes:
- helm chart is better than EKS addons
- AWS Tower Account Factory for Terraform
- prefer linear over JIRA
- buying your own IP

journey of alert
- there are no alerts at all, we need alert
- we have alerts, too many of them, so we ignore them
- we prioritize the alerts, only the critical one wake me up
- ignore the non-critical one