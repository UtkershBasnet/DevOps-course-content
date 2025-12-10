#### Date: 10th December 2025
# Deep Dive into Kubernetes Services - Part 2

## 1. Advanced Service Networking
Building on the basics, let's explore more complex networking patterns and 
resource types that enhance how services function in Kubernetes.

## 2. Ingress vs. Services
While `LoadBalancer` services are great, they can become expensive and 
difficult to manage if you have many services.
- **Ingress:** An API object that manages external access to the services in 
  a cluster, typically HTTP. It can provide load balancing, SSL termination, 
  and name-based virtual hosting.
- **Ingress Controller:** The software that implements the Ingress (e.g., 
  NGINX Ingress Controller, Traefik, HAProxy).

## 3. Network Policies
By default, all pods in a cluster can communicate with each other. Network 
Policies allow you to control traffic flow at the IP address or port level.
- **Isolation:** You can isolate a specific namespace or set of pods.
- **Ingress/Egress Rules:** Define what traffic is allowed *into* (ingress) 
  and *out of* (egress) a pod.

## 4. Multi-Port Services
A service can expose multiple ports. This is useful if a pod runs multiple 
services or needs both HTTP and HTTPS access.
```yaml
ports:
- name: http
  protocol: TCP
  port: 80
  targetPort: 9376
- name: https
  protocol: TCP
  port: 443
  targetPort: 9377
```

## 5. Session Affinity (Sticky Sessions)
If you want a client to always be routed to the same pod, you can use 
`sessionAffinity: ClientIP`. This is useful for stateful applications 
running on multiple pods.

## 6. Service Proxies
The `kube-proxy` runs on every node and is responsible for implementing the 
Service abstraction. It can work in different modes:
- **IPtables Mode:** (Default) Uses Linux IPtables rules to redirect traffic 
  to pods.
- **IPVS Mode:** Uses Linux Virtual Server (IPVS) for load balancing, which is 
  more efficient for clusters with thousands of services.

## 7. Troubleshooting Services
- `kubectl get svc`: List services.
- `kubectl describe svc <name>`: View status, selectors, and endpoints.
- `kubectl get endpoints <name>`: Check if the service actually found pods.
- **Common Issues:**
    - Selector doesn't match pod labels.
    - `targetPort` doesn't match the port the app is listening on.
    - Pod is not "Ready" (Readiness probe failing).

## 8. External Traffic Policy
`externalTrafficPolicy: Local` preserves the client's source IP address and 
avoids an extra hop, but might result in uneven load balancing. 
`externalTrafficPolicy: Cluster` (default) obscures the client IP but 
ensures better load distribution across the cluster.

## 9. Conclusion
Advanced service management involves balancing external access (Ingress), 
security (Network Policies), and performance. Mastering these concepts is 
key to building secure, scalable, and efficient production-grade 
architectures on Kubernetes.

---
*End of Notes*
