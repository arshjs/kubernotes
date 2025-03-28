# Resource Quota

A _**ResourceQuota**_ is a mechanism used to limit the amount of resources (such as CPU, memory, and storage) that can be consumed within a namespace.

### Creation:

```bash
kubectl apply -f resource-quota.yaml
```

### Basic Definition

- Api Version: `v1`
- Kind: `ResourceQuota`
- Shorthand: `rq`

```yaml
apiVersion: v1
kind: ResourceQuota
metadata:
  name: rq
  namespace: ns
spec:
  hard:
    requests.cpu: "4" # CPU cores
    requests.memory: "8Gi"
    limits.cpu: "8"
    limits.memory: "16Gi"
    pods: "10" # Maximum number of pods in ns
  soft:
    requests.cpu: "4"
    requests.memory: "8Gi"
    limits.cpu: "8"
    limits.memory: "16Gi"
    pods: "10"
```

- `hard` limits are the actual enforced limits.
- `soft` limits are more like guidelines and are less commonly used.
