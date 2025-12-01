#### Date: 1st December 2025
# Deep Dive into Kubernetes Pods

## 1. What is a Pod?
A Pod is the smallest, most basic deployable object in Kubernetes. It 
represents a single instance of a running process in your cluster. A pod 
encapsulates one or more containers, storage resources, a unique network IP, 
and options that govern how the container(s) should run.

## 2. Pod Characteristics
- **Ephemeral:** Pods are not intended to be long-lived. If a node fails, the 
  pods on that node are deleted.
- **Atomic Unit:** A pod is either scheduled to a node as a whole or not at 
  all. All containers in a pod run on the same node.
- **Shared Resources:**
    - **Shared Network:** All containers in a pod share the same network 
      namespace (IP address and port space). They can communicate via `localhost`.
    - **Shared Storage:** Pods can specify a set of shared storage volumes 
      that all containers in the pod can mount.

## 3. Why Multiple Containers in a Pod?
The primary use case for multiple containers in a single pod is the 
**Sidecar Pattern**. A helper container (sidecar) assists the main application 
container (e.g., a log shipper, a proxy, or a config reloader).
- **Coupling:** Containers should only be in the same pod if they are 
  tightly coupled and need to share resources.

## 4. Pod Lifecycle and Phases
- **Pending:** The pod has been accepted by the system but is not yet running.
- **Running:** The pod has been bound to a node, and all containers have 
  been created.
- **Succeeded:** All containers in the pod have terminated successfully (exit 0).
- **Failed:** All containers have terminated, and at least one container 
  exited with an error (non-zero exit).
- **Unknown:** The state of the pod cannot be determined.

## 5. Pod Manifest (YAML Example)
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: my-webapp
  labels:
    app: web
spec:
  containers:
  - name: web-container
    image: nginx:latest
    ports:
    - containerPort: 80
```

## 6. Managing Pods with Kubectl
- `kubectl get pods`: List all pods.
- `kubectl describe pod <name>`: Detailed info about a specific pod.
- `kubectl apply -f pod.yaml`: Create or update a pod from a file.
- `kubectl delete pod <name>`: Delete a pod.
- `kubectl exec -it <name> -- /bin/bash`: Open a shell in the first container 
  of a pod.

## 7. Resource Management
You can (and should) specify resource requests and limits for pods:
- **Requests:** Minimum resources required for the pod to run.
- **Limits:** Maximum resources the pod can consume.
```yaml
resources:
  requests:
    memory: "64Mi"
    cpu: "250m"
  limits:
    memory: "128Mi"
    cpu: "500m"
```

## 8. Health Checks (Probes)
- **Liveness Probe:** Checks if the container is still alive. If it fails, K8s 
  restarts the container.
- **Readiness Probe:** Checks if the container is ready to serve traffic. If it 
  fails, K8s stops sending traffic to the pod.
- **Startup Probe:** Checks if the application inside the container has 
  successfully started.

## 9. Conclusion
Pods are the atomic building blocks of Kubernetes. While you rarely create 
individual pods directly in production (instead using controllers like 
Deployments), understanding how pods function is critical for troubleshooting 
and designing distributed systems on Kubernetes.

---
*End of Notes*
