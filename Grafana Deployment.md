---
topic:
  - devops
---
In the payfazz old cluster, there is grafana deployment, the grafana itself is managed by ArgoCD and the manifest itself was the result of helm chart template after the value was injected, it's deployed in https://github.com/payfazz/infra-kubernetes-manifest/blob/22cbd7299c202944cda5914f8ba7742198d9f79c/overlays/k8mgmt0/fazzmon/grafana-statefulset.yaml#L107

the issue was on the mariadb, check the issue here [[Galera MariaDB Issue]]

After we managed to get the Maria DB up and confirm that the database is running, we modify the grafana to be able to use the new database. however there are a bit of an issue, the configuration was injected using kubeseal, and somehow kubeseal is not working for me

I ended up using the vault storage secret to try input new config. and weirdly, the config wasn't working, somehow the config that's there as a secret was wrongly configured and i need to modify it manually to make it working again
