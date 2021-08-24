# Kubernetes.

# Index

* [What is Kubernetes](#What-is-Kubernetes)
* [Kubernate vs Swarm](#Kubernate-vs-Swarm)
	* [Advantages Swarm](#Advantages-Swarm)
	* [Advantages Kubernetes](#Advantages-Kubernetes)
* [Terminology](#Terminology)
* [Commands](#Commands)
* [Services](#Services)
* [Manage Techniques](#Manage-Techniques)


Differences between kubectl, minicube so forth?

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
- `Pod`: One or more containers runnung together on one none, it is the basic unit of deployment. Containers are always in pods.
- `Controller`: For creating/updating pods and other objects. There are many types of `controllers` Deployment, ReplicaSet, StatefulSet, DaemonSet, Job, CronJob, so forth.
- `Service`: Network endpoint to connect a pod.
- `Namespace`: Filtered group of objects in cluster.
- `ReplicaSets` : A ReplicaSet's purpose is to maintain a stable set of replica Pods running at any given time
- `Deploymeny`: 
- `Service`: An abstract way to expose an application running on a set of Pods as a network service.


## Commands

- kubectl

<table>
<thead>
	<tr>
	<th>Commands</th>
	<th>Action</th>
	</tr>
</thead>
<tbody>
	<tr>
		<td>kubectl version</td>
		<td>This command should show the kubernetes versions, for the client and server</td>
	</tr>
	<tr>
		<td>kubectl run <name> --image naginx</td>
		<td>Create a pod via CLI</td>
	</tr>
	<tr>
		<td>kubectl delete <strong>pod name</strong></td>
		<td>List all the pods</td>
	</tr>
	<tr>
		<td>kubectl get pods</td>
		<td>List all the pods</td>
	</tr>
	<tr>
		<td>kubectl create deployment <strong>deployment name</strong> --image <strong>image_name</strong></td>
		<td>Create a deployment</td>
	</tr>
	<tr>
		<td>kubectl scale <strong>deployment name</strong> --replicas <strong>amount_replicas</strong></td>
		<td>Scale replicas</td>
	</tr>
	<tr>
		<td>kubectl logs <strong>deployment name</strong></td>
		<td>See the logs in a specific deployment</td>
	</tr>
	<tr>
		<td>kubectl logs <strong>deployment name</strong></td>
		<td>See the logs in a specific deployment</td>
	</tr>
</tbody>
</table>

## Services 

An abstract way to expose an application running on a set of Pods as a network service.

If we want to connec to pods we need a service.

CoreDNS allow us to resolve services by name.

### Cluster IP

- Single, internal virtual IP allocated
- Only reachable within cluster (nodes and pods)
- Pods can reach service on apps port number
- Available in Kubernetes


<table>
<thead>
	<tr>
	<th>Commands</th>
	<th>Action</th>
	</tr>
</thead>
<tbody>
	<tr>
		<td>kubectl expose <strong> deployment name</strong>  --port <strong>port_number</strong></td>
		<td>Create ClusterIp Service</td>
	</tr>
</tbody>
</table>

### Node Port

- High port allocated on each node
- Port is open on every node's ip
- Anyone can connect(If they can reach the node)
- Available in Kubernetes

<table>
<thead>
	<tr>
	<th>Commands</th>
	<th>Action</th>
	</tr>
</thead>
<tbody>
	<tr>
		<td>kubectl expose <strong> deployment name</strong>  --port <strong>port_number</strong> --name <strong> service_name</strong> --type <strong>NodePort</strong></td>
		<td>Create ClusterIp Service</td>
	</tr>
</tbody>
</table>

### LoadBalancer 

- Controls a LB endpoint external to the cluster.
- Only Available when infra provider gives you a LB (AWS ELB, etc)

### External Name

- Adds CNAME DNS Record to CoreDNS only.
- It is not using so often

## Manage Techniques

Manage Techniques are the strategies that we can use when we are setting up our kubernetes.

### Imperative

WIth the `imperative` style we are using kubernetes always thinking in `how` to achieve the purpose. Usually we use imperative approach when we run sinble commands like `run`, `expose`, `scale`, `edit`, `create` so forth. 

- The imperative style is better for dev/learning/personal projects
- Easy to learn, hardest to manager over time.
- Usually we need to know the state of our deployments in order to use imperative style.

### Declarative Style

The `declarative` style focus in `what` to do instead in how to do it. In order to use a `declarative` approach we need to use `yaml` in order to config our deployments.

- Best for prod, easier to automate.
- Harder to understand and predict changes

### Imperative Objects

The `imperative objects` is middle point between `imperative` and `declarative`, and basically is create little `yaml` object for every single command.

- Good for prod of small environments, single file per command.
- Store your changes in git-bases yaml files
- Hard to automate