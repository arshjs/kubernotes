# Replica Set

> A ReplicaSet is a controller that ensures a specified number of identical pods are running at any given time.

Shorthand: `rs`

Creation:

- `kubectl apply -f replica-set.yaml`
- `kubectl create rs replica-set --image=nginx --replicas=3 --dry-run=client`

## Basic Definition

- apiVersion: `apps/v1`
- kind: `ReplicaSet`

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
