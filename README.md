# hackthur-kluster

## Commands
```bash
docker exec reverent_chatterjee kubectl get replicaset -n default
NAME                   DESIRED   CURRENT   READY   AGE
nginx-lab-56cb7cbcb4   1         1         1       28m
nginx-lab-599b6f8f9    0         0         0       28m
nginx-lab-6889885447   0         0         0       33m


docker exec -it reverent_chatterjee bash
kubectl get replicaset -n default
NAME                   DESIRED   CURRENT   READY   AGE
nginx-lab-56cb7cbcb4   1         1         1       32m
nginx-lab-599b6f8f9    0         0         0       33m
nginx-lab-6889885447   0         0         0       37m

```
