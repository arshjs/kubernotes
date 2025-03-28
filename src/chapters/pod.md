# Pod

A _**Pod**_ is the smallest and most basic unit of deployment in Kubernetes.

### Creation:

```bash
kubectl apply -f pod.yaml
```

```bash
kubectl create po nginx --image=nginx --dry-run=client
```

### Basic Definition

- Api Version: `v1`
- Kind: `Pod`
- Shorthand: `po`

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: nginx
  namespace: ns
  labels:
    app: my-app
spec:
  containers:
    - name: nginx
      image: nginx
      resources:
        limits:
          cpu: "0.5" # half a core
          memory: "20Mi" # 20 mebibytes
        requests:
          cpu: "0.35" # 35% of a core
          memory: "10Mi" # 20 mebibytes
```

### Security Context

- Used to define security settings for a pod and its containers
- The security context of the container (`pod.spec.containers.securityContext`) overrides the Pod level security context (`pod.spec.securityContext`)
- Both security contexts are `{}` by default

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: nginx
~  namespace: ns
~  labels:
~    app: my-app
spec:
  securityContext:
    runAsUser: 1000
    runAsGroup: 1000
    runAsNonRoot: true
  containers:
    - name: nginx
      image: nginx
~      resources:
~        limits:
~          cpu: "0.5" # half a core
~          memory: "20Mi" # 20 mebibytes
~        requests:
~          cpu: "0.35" # 35% of a core
~          memory: "10Mi" # 20 mebibytes
      securityContext:
        runAsUser: 2000
        readOnlyRootFilesystem: true
```

### Resource Limits and Requests

- Resource Requests is the amount of CPU or memory that Kubernetes will reserve for the container
- Resource Limits is the maximum amount of CPU or memory that the container can use

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: nginx
~  namespace: ns
~  labels:
~    app: my-app
spec:
~  securityContext:
~    runAsUser: 1000
~    runAsGroup: 1000
~    runAsNonRoot: true
  containers:
    - name: nginx
      image: nginx
      resources:
        limits:
          cpu: "0.5" # half a core
          memory: "20Mi" # 20 mebibytes
        requests:
          cpu: "0.35" # 35% of a core
          memory: "10Mi" # 20 mebibytes
~      securityContext:
~        runAsUser: 2000
~        readOnlyRootFilesystem: true
```
