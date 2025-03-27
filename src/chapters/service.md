# Service

A Kubernetes Service enables communication between different parts of your application and handles the networking aspects for you.

It provides stable access to pods, even as they get created, destroyed, or replaced, ensuring high availability.

### Creation:

```bash
kubectl apply -f service.yaml
```

```bash
kubectl create svc clusterip back-end --tcp=80:8080 --dry-run=client
```

```bash
kubectl create svc nodeport my-service --tcp=80:8080 --type=NodePort --node-port=30008 --dry-run=client
```

### Basic Definition

- apiVersion: `apps/v1`
- kind: `Service`
- Shorthand: `svc`
- Default `spec.type` is `ClusterIP`

### Service Types

#### NodePort

Used to expose service externally accessed via `<Node-IP>:<Node-Port>`

```yaml
apiVersion: v1
kind: Service
metadata:
  name: my-service
spec:
  type: NodePort
  ports:
    - targetPort: 8080
      port: 80
      nodePort: 30008 # default 30000 - 32767
  selector:
    app: my-app
```

#### ClusterIP

Used to expose service internally in the cluster at the given port

```yaml
apiVersion: v1
kind: Service
metadata:
  name: back-end
spec:
  type: ClusterIP
  ports:
    - targetPort: 8080
      port: 80
  selector:
    app: back-end
```

#### Load Balancer

- Only works with supported cloud platforms, eg. GCP, AWS, AZURE
- On unsupported platforms works like node-port
