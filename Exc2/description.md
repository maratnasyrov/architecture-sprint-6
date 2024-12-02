# Результаты работы

`kubectl top pod`:

```shell
NAME                            CPU(cores)   MEMORY(bytes)
scaletestapp-7cfcb7b885-42s5t   1m           2Mi
scaletestapp-7cfcb7b885-6dl59   1m           10Mi
scaletestapp-7cfcb7b885-9xhmp   4m           26Mi
```

`kubectl describe deployment scaletestapp`:

```shell
Name:                   scaletestapp
Namespace:              default
CreationTimestamp:      Mon, 02 Dec 2024 05:35:40 +0100
Labels:                 app=scaletestapp
Annotations:            deployment.kubernetes.io/revision: 1
Selector:               app=scaletestapp
Replicas:               3 desired | 3 updated | 3 total | 3 available | 0 unavailable
StrategyType:           RollingUpdate
MinReadySeconds:        0
RollingUpdateStrategy:  25% max unavailable, 25% max surge
Pod Template:
  Labels:  app=scaletestapp
  Containers:
   scaletestapp:
    Image:      shestera/scaletestapp
    Port:       8080/TCP
    Host Port:  0/TCP
    Limits:
      memory:  30Mi
    Requests:
      memory:      20Mi
    Environment:   <none>
    Mounts:        <none>
  Volumes:         <none>
  Node-Selectors:  <none>
  Tolerations:     <none>
Conditions:
  Type           Status  Reason
  ----           ------  ------
  Progressing    True    NewReplicaSetAvailable
  Available      True    MinimumReplicasAvailable
OldReplicaSets:  <none>
NewReplicaSet:   scaletestapp-7cfcb7b885 (3/3 replicas created)
Events:
  Type    Reason             Age    From                   Message
  ----    ------             ----   ----                   -------
  Normal  ScalingReplicaSet  31m    deployment-controller  Scaled up replica set scaletestapp-7cfcb7b885 to 1
  Normal  ScalingReplicaSet  5m38s  deployment-controller  Scaled up replica set scaletestapp-7cfcb7b885 to 2 from 1
  Normal  ScalingReplicaSet  4m38s  deployment-controller  Scaled up replica set scaletestapp-7cfcb7b885 to 3 from 2
```

Видим по событиям, что сначала лимит реплик был поднят до трёх, а через 2 минуты до пяти. В это время продолжалась
работа Locust с RPS 312.
