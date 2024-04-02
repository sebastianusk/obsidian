---
tags:
  - zettelkasten
topic:
  - devops
createAt: 2024-03-31 15:21
---
Basically, it's a way for Kubernetes to control anything, literally anything.
1. Define the CRD, it's a way to tell the Kubernetes declaratively
2. build the controller. it's to watch and make sure the workload is running in the intended way.