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


### Commands to check for replicaset and its versions

```bash
## check for the history
kubectl rollout history deployment/api -n my-namespace

## modify the deployment (do not use it in production environment)
kubectl rollout undo deployment/api -n my-namespace

kubectl delete pod nginx-lab-56cb7cbcb4-krrc8


❯ kubectl describe replicaset nginx-lab-56cb7cbcb4
Name:           nginx-lab-56cb7cbcb4
Namespace:      default
Selector:       pod-template-hash=56cb7cbcb4,workload.user.cattle.io/workloadselector=apps.deployment-default-nginx-lab
Labels:         pod-template-hash=56cb7cbcb4
                workload.user.cattle.io/workloadselector=apps.deployment-default-nginx-lab
Annotations:    deployment.kubernetes.io/desired-replicas: 1
                deployment.kubernetes.io/max-replicas: 2
                deployment.kubernetes.io/revision: 3
Controlled By:  Deployment/nginx-lab
Replicas:       1 current / 1 desired
Pods Status:    1 Running / 0 Waiting / 0 Succeeded / 0 Failed
Pod Template:
  Labels:       pod-template-hash=56cb7cbcb4
                workload.user.cattle.io/workloadselector=apps.deployment-default-nginx-lab
  Annotations:  cattle.io/timestamp: 2026-10-12T04:38:01Z
                kubectl.kubernetes.io/restartedAt: 2026-10-12T04:38:01Z
  Containers:
   nginx:
    Image:         nginx:stable
    Port:          80/TCP (http)
    Host Port:     0/TCP (http)
    Environment:   <none>
    Mounts:        <none>
  Volumes:         <none>
  Node-Selectors:  <none>
  Tolerations:     <none>
Events:            <none>

```



### GitOps

```bash
❯ kubectl get pods -A
NAMESPACE                   NAME                                                  READY   STATUS      RESTARTS     AGE
cattle-capi-system          capi-controller-manager-754dcdb8b9-qr25z              1/1     Running     1 (8h ago)   24h
cattle-fleet-local-system   fleet-agent-9bb754f4c-dpfkn                           1/1     Running     1 (8h ago)   24h
cattle-fleet-system         fleet-controller-996dc8bf6-qs9l4                      3/3     Running     6 (8h ago)   24h
cattle-fleet-system         gitjob-59645648f-pk47x                                1/1     Running     4 (8h ago)   24h
cattle-fleet-system         helmops-545cb597d9-6czlv                              1/1     Running     1 (8h ago)   24h
cattle-system               api-extension-9bc6c988d-q2b6b                         1/1     Running     1 (8h ago)   24h
cattle-system               rancher-webhook-74cf67bb99-hrgkw                      1/1     Running     1 (8h ago)   24h
cattle-system               system-upgrade-controller-5dc7c44677-5tfzj            1/1     Running     1 (8h ago)   23h
cattle-turtles-system       rancher-turtles-controller-manager-74867b76f8-db2hm   1/1     Running     1 (8h ago)   24h
default                     nginx-lab-56cb7cbcb4-krrc8                            1/1     Running     0            3h32m
fleet-local                 rke2-machineconfig-cleanup-cronjob-29862725-zxk29     0/1     Completed   0            8h
kube-system                 coredns-5f5694d56b-tjxzh                              1/1     Running     1 (8h ago)   24h
❯ kubectl get pods -n cattle-fleet-system
NAME                               READY   STATUS    RESTARTS     AGE
fleet-controller-996dc8bf6-qs9l4   3/3     Running   6 (8h ago)   24h
gitjob-59645648f-pk47x             1/1     Running   4 (8h ago)   24h
helmops-545cb597d9-6czlv           1/1     Running   1 (8h ago)   24h

```



## Fleet with Drift

```yml
spec:
  correctDrift:
    enabled: true
```




Tres elementos para la arquitectura

namespace => responsabilidad

cattle-fleet-system => ejecutar los controladores centrales de fleet
fleet-local => almacenar recursos de gestion de fleet dentro del cluster local, como nuestro nuveo futuro GitOp
default =>  aloja nuestra app nginx

