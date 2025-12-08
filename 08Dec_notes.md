#### Date: 8th December 2025
# Understanding Kubernetes Services - Part 1

## 1. Why do we need Services?
Pods in Kubernetes are ephemeral. When a pod is destroyed and recreated, it 
gets a new IP address. This makes it difficult for other components (like 
a frontend) to reliably communicate with a set of pods (like a backend).
- **Service** provides a stable IP address and DNS name for a logical set of 
  Pods.
- **Service Discovery:** Services allow pods to find each other without 
  knowing their individual IPs.
- **Load Balancing:** Services automatically distribute traffic across all 
  matching pods.

## 2. How Services Work
Services use **Selectors** to identify the set of Pods they should target. 
If a Pod has labels that match the Service's selector, it is included in the 
Service's endpoints.
- **Endpoints:** A list of IP addresses and ports of the pods that currently 
  match the service's selector. K8s keeps this list updated automatically.

## 3. Service Types
Kubernetes supports four main types of Services:
1. **ClusterIP (Default):** Exposes the service on a cluster-internal IP. 
   Accessible only from within the cluster.
2. **NodePort:** Exposes the service on each Node's IP at a static port. 
   Accessible from outside the cluster using `<NodeIP>:<NodePort>`.
3. **LoadBalancer:** Exposes the service externally using a cloud provider's 
  load balancer (e.g., AWS ELB, GCP Cloud Load Balancing).
4. **ExternalName:** Maps the service to the contents of the `externalName` 
  field (e.g., `foo.bar.example.com`).

## 4. Service Manifest (YAML Example - ClusterIP)
```yaml
apiVersion: v1
kind: Service
metadata:
  name: my-backend-service
spec:
  selector:
    app: backend
  ports:
    - protocol: TCP
      port: 80         # Port the service listens on
      targetPort: 8080 # Port the container listens on
  type: ClusterIP
```

## 5. Port Mapping Explained
- **Port:** The port that clients within the cluster use to access the 
  service.
- **TargetPort:** The port on the pod that the service forwards traffic to.
- **NodePort:** (Only for NodePort type) The port exposed on all nodes (range 
  30000-32767).

## 6. Accessing Services
- **Environment Variables:** K8s sets environment variables for each active 
  service on every pod in the same namespace.
- **DNS (Recommended):** K8s runs a DNS service (CoreDNS) that allows you to 
  access services by their name (e.g., `my-service.my-namespace.svc.cluster.local`).

## 7. Headless Services
A headless service is a service with `clusterIP: None`. Instead of load 
balancing, it returns the IP addresses of all matching pods directly. Useful 
for stateful applications where you need to communicate with specific pods.

## 8. Conclusion
Services are the glue that holds Kubernetes applications together. They 
provide the stability and discovery mechanisms needed for microservices to 
communicate reliably in a dynamic, containerized environment.

---
*End of Notes*
