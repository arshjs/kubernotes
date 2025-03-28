# Deployment

A _**Deployment**_ is a higher-level abstraction that manages a set of pods and ensures that they are running in a desired state.

### Creation:

```bash
kubectl apply -f deployment.yaml
```

```bash
kubectl create deploy nginx --image=nginx --dry-run=client
```

### Basic Definition

- apiVersion: `apps/v1`
- kind: `Deployment`
- Shorthand: `deploy`

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx
  namespace: ns
  labels:
    app: my-app
spec:
  selector:
    matchLabels:
      app: my-app
  replicas: 3
  template:
    metadata:
      name: nginx
      labels:
        app: my-app
    spec:
      containers:
        - name: nginx
          image: nginx
          ports:
            - containerPort: 80
```
