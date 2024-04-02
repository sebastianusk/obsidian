---
tags:
  - zettelkasten
topic:
  - devops
createAt: 2024-03-31 14:33
---
Kubernetes is a container orchestrator. We configure it declaratively and it will try to run the application following the configuration and it will help to manage any drift from the expected condition.
# Kubernetes Resources
- Pod, one item of container or set of container (sidecar)
- ReplicaSet manages the replicas of pods, it should be stateless. Usually created by Deployment, where it can manage the rollout and pod spec.
- StatefulSet manages the pod that is supposed to be stateful, maintains its identity and data attached to it
- DaemonSet, application that run in the Node
- Service is a way for Kubernetes to expose it's deployment, there are three types of service:
	- Cluster (just inside of the cluster)
	- Node (all nodes will have it)
	- Load Balancer (usually it's connected to the cloud load balancer)
- Ingress is a concept that control the traffic getting into the cluster. it's implementation if following the ingress controller implementation like NGINX, Contour, etc
# Kubernetes Component
- etcd, the core storage to store the state of the kubernetes
- api server, interface for the etcd, all components are communicate through api server
- scheduler & kubelet. scheduler is located at the center, it's basically watch the pods that's not assigned to a node and assign them. Kubelet is located at the nodes and giving update about the nodes inside of it
- controller, a set of application that's used to maintain the state of the cluster and help to manage actions to correct them
- kubeproxy, deployed in each node and helps to manage the communication between kubernetes workload
# Advance Topics:
- [[Kubernetes Admission Controller]]
- [[Kubernetes Custom Resource Definition]]