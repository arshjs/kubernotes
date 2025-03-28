# Replica Set

A _**ReplicaSet**_ is a controller that ensures a specified number of identical pods are running at any given time.

### Creation:

```bash
kubectl apply -f replica-set.yaml
```

```bash
kubectl create rs replica-set --image=nginx --replicas=3 --dry-run=client
```

### Basic Definition

- Api Version: `apps/v1`
- kind: `ReplicaSet`
- Shorthand: `rs`

```yaml
apiVersion: apps/v1
kind: ReplicaSet
metadata:
  name: replica-set
  namespace: ns
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
          image: nginx
          ports:
            - containerPort: 80
```
