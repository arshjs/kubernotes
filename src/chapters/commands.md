# Commands

- `kubectl get`
    - `kubectl get pods` or `kubectl get pods -o wide`
    - `kubectl get replicasets`
    - `kubectl get all`
- `kubectl delete`
    - `kubectl delete pod [...pod-names]`
    - `kubectl delete replicaset [...replicaset-names]` or `kubectl delete rs [...replicaset-names]`
    - `kubectl delete <resource> --all`
- `kubectl create`
    - `kubectl create -f <resource-manifest>.yaml`
- `kubectl scale`
    - `kubectl scale --replicas=<no-of-replicas> replicaset <replicaset-name>` or `kubectl scale --replicas=<no-of-replicas> rs <replicaset-name>`
- `kubectl describe`
    - `kubectl describe <resource> <resource-name>`
    - `kubectl describe pod <pod-name>`
    - `kubectl describe replicaset <replicaset-name>` or `kubectl describe rs <replicaset-name>`
- `kubectl explain`
    - `kubectl explain <resource>`
- `kubectl edit`
    - `kubectl edit <resource> <resource-name>`
- `kubectl rollout`
    - `kubectl rollout status deployment <deployment-name>`
    - `kubectl rollout history deployment <deployment-name>`
    - `kubectl rollout undo deployment <deployment-name>`
- `kubectl top`
    
    > The `top` command is similar to the native Linux `top` command for measuring CPU and memory usage of processes. You can monitor at the node or pod level.
    > 
    - `kubectl top pods`
    - `kubectl top nodes`