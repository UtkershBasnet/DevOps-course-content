#### Date: 24th November 2025
# Introduction to Orchestration Using Kubernetes

## 1. Why Orchestration?
While Docker is great for managing individual containers, running a 
large-scale application in production involves managing hundreds or 
thousands of containers. Orchestration tools automate:
- Deployment and replication of containers.
- Scaling out or scaling in based on demand.
- Load balancing between container instances.
- Health monitoring and self-healing (restarting failed containers).
- Rolling updates and rollbacks without downtime.
- Service discovery and networking.

## 2. What is Kubernetes?
Kubernetes (K8s) is an open-source container orchestration platform 
originally developed by Google. It provides a framework to run distributed 
systems resiliently. It takes care of scaling and failover for your 
application, provides deployment patterns, and more.

## 3. Kubernetes Architecture

### Control Plane (The Brain)
- **API Server:** The entry point for all commands (kubectl).
- **etcd:** A consistent and highly-available key-value store used as 
  Kubernetes' backing store for all cluster data.
- **Scheduler:** Matches pods to nodes based on resource requirements.
- **Controller Manager:** Runs controller processes (Node, Replication, 
  Endpoints, etc.).

### Worker Nodes (The Brawn)
- **Kubelet:** An agent that runs on each node in the cluster. It ensures that 
  containers are running in a pod.
- **Kube-proxy:** A network proxy that runs on each node, maintaining 
  network rules and allowing communication to your pods.
- **Container Runtime:** The software that is responsible for running 
  containers (e.g., Docker, containerd, CRI-O).

## 4. Basic K8s Objects
- **Pod:** The smallest deployable unit in K8s. A pod can contain one or more 
  containers.
- **Service:** An abstract way to expose an application running on a set of 
  Pods as a network service.
- **Namespace:** Virtual clusters within a physical cluster to organize and 
  isolate resources.
- **Volume:** A directory containing data, accessible to the containers in a 
  pod.

## 5. Declarative Management
Kubernetes works on a declarative model. You define the "desired state" of your 
cluster in YAML or JSON files, and Kubernetes works to maintain that state.
- **Imperative:** "Run 3 instances of this container."
- **Declarative:** "I want 3 instances of this container to be running at all 
  times."

## 6. Basic Kubectl Commands
- `kubectl get nodes`: List all nodes in the cluster.
- `kubectl get pods`: List pods in the current namespace.
- `kubectl apply -f <file.yaml>`: Create or update resources defined in a file.
- `kubectl describe <resource> <name>`: Show detailed info about a resource.
- `kubectl logs <pod_name>`: View logs of a specific pod.
- `kubectl delete <resource> <name>`: Delete a resource.

## 7. Main Benefits of K8s
- **High Availability:** Automatically restarts failed containers.
- **Scalability:** Horizontal scaling is easy and automated.
- **Efficiency:** Better resource utilization by packing containers onto nodes.
- **Portability:** K8s runs the same way on-premise as it does in any cloud 
  (AWS, GCP, Azure).

## 8. Conclusion
Kubernetes has become the industry standard for container orchestration. Its 
robust feature set and wide adoption make it the go-to choice for managing 
complex, cloud-native applications at scale.

---
*End of Notes*
