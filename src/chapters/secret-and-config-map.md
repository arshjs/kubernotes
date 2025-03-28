# Secret & Config Map

Kubernetes provides two key resources to manage configuration data for applications.

## ConfigMap

A _**ConfigMap**_ enables decoupling of configuration artifacts from application code, making it easier to manage configurations across different environments.

Used to store non-sensitive configuration data (e.g., environment variables, configuration files).

### Creation

```bash
kubectl apply -f config-map.yaml
```

```bash
kubectl create configmap my-config --from-literal=APP_ENV=production --from-literal=LOG_LEVEL=info
```

### Basic Definition

- Api Version: `v1`
- Kind: `ConfigMap`
- Shorthand: `cm`

```yaml
apiVersion: v1
kind: ConfigMap
metadata:
  name: my-config
data:
  APP_ENV: "production"
  APP_DEBUG: "false"
  LOG_LEVEL: "info"
```

- The `data` section contains key-value pairs that store configuration settings.

### Using ConfigMap in a Pod

#### Method 1: Using ConfigMap as Environment Variables

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: my-pod
spec:
  containers:
    - name: my-container
      image: nginx
      envFrom:
        - configMapRef:
            name: my-config
```

- This will inject the ConfigMap values as environment variables in the container

#### Method 2: Mounting ConfigMap as a File

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: my-pod
spec:
  containers:
    - name: my-container
      image: nginx
      volumeMounts:
        - name: config-volume
          mountPath: "/etc/config"
  volumes:
    - name: config-volume
      configMap:
        name: my-config
```

- The ConfigMap data will be available as files in `/etc/config/`

---

## Secret

A _**Secret**_ is similar to a ConfigMap but is designed to store sensitive information (e.g., passwords, API keys, certificates) securely.

The data in a Secret is **base64-encoded** for security purposes.

### Creation

```bash
kubectl apply -f my-secret.yaml
```

```bash
kubectl create secret generic my-secret --from-literal=DB_USER=username --from-literal=DB_PASSWORD=password
```

You can encode values using:

```bash
echo -n "username" | base64
echo -n "password" | base64
```

### Basic Definition

- Api Version: `v1`
- Kind: `Secret`
- Shorthand: `cm`

```yaml
apiVersion: v1
kind: Secret
metadata:
  name: my-secret
type: Opaque
data:
  DB_USER: dXNlcm5hbWU= # "username" in base64
  DB_PASSWORD: cGFzc3dvcmQ= # "password" in base64
```

### Using Secrets in a Pod

#### Method 1: Using Secrets as Environment Variables

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: my-pod
spec:
  containers:
    - name: my-container
      image: nginx
      env:
        - name: DB_USER
          valueFrom:
            secretKeyRef:
              name: my-secret
              key: DB_USER
        - name: DB_PASSWORD
          valueFrom:
            secretKeyRef:
              name: my-secret
              key: DB_PASSWORD
```

- The Secret values will be exposed as environment variables inside the container

#### Method 2: Mounting Secrets as Files

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: my-pod
spec:
  containers:
    - name: my-container
      image: nginx
      volumeMounts:
        - name: secret-volume
          mountPath: "/etc/secrets"
  volumes:
    - name: secret-volume
      secret:
        secretName: my-secret
```

- The Secret values will be available as files in `/etc/secrets/`

---

### ConfigMap vs. Secret

| Feature         | ConfigMap                           | Secret                               |
| --------------- | ----------------------------------- | ------------------------------------ |
| Use Case        | Non-sensitive data                  | Sensitive data (passwords, API keys) |
| Storage Type    | Plain text                          | Base64-encoded                       |
| Data Size Limit | Large (can store full config files) | Small (meant for sensitive data)     |
| Mounting Method | Env variables, files                | Env variables, files                 |
