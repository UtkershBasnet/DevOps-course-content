#### Date: 5th December 2025
# Deep Dive into Kubernetes Deployments

## 1. What is a Deployment?
A Deployment provides declarative updates for Pods and ReplicaSets. You 
describe a *desired state* in a Deployment, and the Deployment Controller 
changes the actual state to the desired state at a controlled rate.

## 2. Key Features of Deployments
- **Declarative Updates:** Define the end state, and K8s makes it happen.
- **Self-Healing:** If a pod or node fails, the Deployment ensures the 
  replicas are replaced.
- **Scaling:** Easily scale the number of replicas up or down.
- **Rolling Updates:** Update your application to a new version without 
  downtime.
- **Rollbacks:** Quickly revert to a previous version if an update fails.
- **Pause/Resume:** Pause a deployment to make multiple changes before 
  triggering a rollout.

## 3. How Deployments Manage ReplicaSets
When you create a Deployment, it creates a ReplicaSet to manage the pods. 
When you update the Deployment (e.g., change the image version), it 
creates a *new* ReplicaSet and slowly scales it up while scaling down 
the *old* ReplicaSet. This is how rolling updates are achieved.

## 4. Deployment Manifest (YAML Example)
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deployment
spec:
  replicas: 3
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
      - name: nginx
        image: nginx:1.14.2
        ports:
        - containerPort: 80
```

## 5. Deployment Strategies
- **RollingUpdate (Default):** Slowly replaces old pods with new ones. You can 
  tune this with `maxSurge` (how many extra pods) and `maxUnavailable` (how 
  many pods can be down during update).
- **Recreate:** Kills all old pods before starting any new ones. Causes 
  downtime but useful if two versions cannot run simultaneously.

## 6. Managing Deployments with Kubectl
- `kubectl apply -f deployment.yaml`: Create or update.
- `kubectl get deployments`: List all deployments.
- `kubectl rollout status deployment/<name>`: Check the progress of an update.
- `kubectl rollout history deployment/<name>`: See previous versions.
- `kubectl rollout undo deployment/<name>`: Roll back to the previous version.
- `kubectl scale deployment/<name> --replicas=10`: Scale manually.

## 7. Rollback Mechanism
Kubernetes keeps the old ReplicaSets (by default, it keeps the last 10). 
This allows for near-instant rollbacks. The old ReplicaSet is simply 
scaled back up while the current one is scaled down.

## 8. Best Practices
- **Use meaningful labels** for selectors.
- **Set resource requests and limits** for all containers.
- **Use Readiness Probes** to ensure pods are ready before taking traffic 
  during a rolling update.
- **Keep Deployment manifests in Git** (GitOps) for version control.

## 9. Conclusion
Deployments are the workhorse of Kubernetes. They provide the abstraction needed 
to manage application lifecycles, ensuring high availability, scalability, and 
smooth updates in a production environment.

---
*End of Notes*
