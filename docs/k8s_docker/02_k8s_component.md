---
sidebar_position: 2
---

# K8s Component

- ### Master Node Components
	- API Server: The front-end for the Kubernetes control plane. It exposes the Kubernetes API and serves as the entry point for all REST commands used to control the cluster.
	- Controller Manager: Governs controllers, which are background processes that manage the state of the cluster (e.g., managing nodes, replicas).
	- Scheduler: Assigns work to nodes by selecting which node will run a new pod based on resource availability and constraints.
	- etcd: A distributed key-value store used for storing all cluster data, including configuration data and state information.

- ### Worker Node Components
	- Kubelet: An agent that runs on each worker node, responsible for managing pods and ensuring that containers are running as expected.
	- Kube Proxy: Manages network routing for services. It facilitates communication between different services and pods by maintaining network rules on nodes.
	- Container Runtime: The software responsible for running containers. Common container runtimes include Docker, containerd, and CRI-O.
