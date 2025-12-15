#### Date: 15th December 2025
# Understanding HPA (Horizontal Pod Autoscaler)

## 1. What is Scaling?
In cloud computing, scaling is the ability to adjust resources to meet 
fluctuating demand.
- **Vertical Scaling (Scaling Up):** Increasing the CPU/Memory of existing 
  nodes/pods.
- **Horizontal Scaling (Scaling Out):** Adding more instances (pods) of 
  your application.

## 2. Horizontal Pod Autoscaler (HPA)
HPA automatically scales the number of Pods in a replication controller, 
deployment, replica set, or stateful set based on observed CPU utilization (or, 
with custom metrics support, on some other application-provided metrics).

## 3. How HPA Works
HPA works as a control loop (default 15 seconds):
1. **Query Metrics:** HPA queries the Metrics Server for resource usage of 
   the pods targeted by the deployment.
2. **Calculate Replicas:** It compares the current usage against the 
   target usage defined in the HPA manifest.
3. **Scale:** If needed, it updates the replica count in the deployment's 
   specification.

## 4. HPA Manifest (YAML Example)
```yaml
apiVersion: autoscaling/v2
kind: HorizontalPodAutoscaler
metadata:
  name: php-apache
spec:
  scaleTargetRef:
    apiVersion: apps/v1
    kind: Deployment
    name: php-apache
  minReplicas: 1
  maxReplicas: 10
  metrics:
  - type: Resource
    resource:
      name: cpu
      target:
        type: Utilization
        averageUtilization: 50
```

## 5. Prerequisites for HPA
- **Metrics Server:** Must be installed in the cluster to provide resource 
  usage data.
- **Resource Requests:** The pods must have CPU and/or Memory *requests* 
  defined. HPA cannot calculate percentage utilization without a base value.

## 6. Scaling on Custom Metrics
Beyond CPU and Memory, HPA can scale based on:
- **Object Metrics:** (e.g., number of requests per second on an Ingress).
- **Pod Metrics:** (e.g., specific application-exposed metric).
- **External Metrics:** (e.g., number of messages in a cloud queue).

## 7. Scaling Cooldowns (Stabilization Window)
To prevent "flapping" (rapidly scaling up and down), HPA has a stabilization 
window. By default, it waits for a few minutes before scaling down after 
a spike has passed.

## 8. Troubleshooting HPA
- `kubectl get hpa`: Show current status (targets, replicas).
- `kubectl describe hpa <name>`: View events and scaling history.
- **Common Issues:**
    - Metrics Server not installed.
    - Resource requests not defined in the deployment.
    - Target metric name is incorrect.

## 9. Conclusion
HPA is a powerful tool for building resilient and cost-effective 
applications. By automatically adjusting capacity to match load, it ensures 
good performance during peaks and saves costs during low-demand periods, 
embodying the core elasticity of the cloud.

---
*End of Notes*
