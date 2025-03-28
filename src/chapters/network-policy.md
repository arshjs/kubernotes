# Network Policy

A _**NetworkPolicy**_ is a specification that controls the networking behavior between pods.

### Creation:

```bash
kubectl apply -f network-policy.yaml
```

```bash
kubectl create netpol allow-ingress-egress --dry-run=client \
  --ingress \
    --from podSelector=app=frontend \
    --ports 80,443 \
  --egress \
    --to ipBlock="192.168.1.0/24" \
    --ports 53
```

### Basic Definition

- Api Version: `networking.k8s.io/v1`
- Kind: `NetworkPolicy`
- Shorthand: `netpol`
- Network policies are namespaced and need plugin like Calico, Cilium, Weave, etc. to work

```yaml
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
  name: allow-ingress-egress
spec:
  podSelector: {}
  ingress:
    - from:
        - podSelector:
            matchLabels:
              app: frontend
      ports:
        - protocol: TCP
          port: 80
        - protocol: TCP
          port: 443
  egress:
    - to:
        - ipBlock:
            cidr: 192.168.1.0/24
      ports:
        - protocol: UDP
          port: 53
  policyTypes:
    - Ingress
    - Egress
```
