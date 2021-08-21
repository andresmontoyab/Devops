# Kubernetes.

# Index

* [What is Kubernetes](#What-is-Kubernetes)
* [Kubernate vs Swarm](#Kubernate-vs-Swarm)
	* [Advantages Swarm](#Advantages-Swarm)
	* [Advantages Kubernetes](#Advantages-Kubernetes)
* [Terminology](#Terminology)
* [Commands](#Commands)

## What is Kubernetes

- Popular Container Orchestrator
- Make many servers act like one
- Many cloud provide it for you

## Kubernate vs Swarm

- Kubernetes and Swarm are both container orchestrators
- Swarm: Easier to deploy/manage
- Kubernates: More features and flexibility

### Advantages Swarm

- Comes with Docker, single vendor container platform
- Easiest orchestrator to deploy/manage yourself
- Follow 80/20 rule, 20% of features for 80% of use cases
- Runs anywhere Docker does
- Secure by default

### Advantages Kubernetes

- Clouds will deploy/manage kubernetes for you
- Infrastructure vendors are making their own distribution
- Flexible: Covers widest set of use cases

## Terminology

- `Kubernetes`: The whole orchestration system
- `K8s`: Also means Kubernetes
- `kubectl`: CLI to configure kuberentes and manage apps
- `cube control`: It is the same kubectl, just another pronunciation
- `Node`: Sigle server in the kubernetes cluster
- `Kubelet`: Kubernetes agent running on nodes
- `Control Plane`: Set of containers that manage the cluster

