# Scaling Application in Kubernetes using Replication Controller

**App Scaling**

➢ Application scalability is the potential of an application to grow in time, being able to efficiently handle more and more requests per minute (RPM).

➢ In kubernetes, user can scale Pods.

➢ Pods can be scale Vertically or Horizontally.

**Stateless Applications**

➢ A stateless application is one that does not store client data from one session to the next. Each request from a client is handled independently, and no session information is retained between different requests.

➢ Stateless applications can be scaled horizontally, meaning new instances (Pods) can be created to handle more load without any dependency on previous requests.

_Examples:_ Web servers, front-end applications.

**Stateful Applications**

➢ A stateful application is one that remembers client data (session information or state) across requests. The state of the application (such as database connections or user session data) is maintained even after the session ends.

➢ Stateful applications are typically scaled vertically (adding more resources to a single instance). However, stateful workloads can also be scaled horizontally with careful orchestration of persistent storage.

_Examples:_ Databases (e.g., MySQL, MongoDB), distributed systems like Kafka or Redis.

**Scaling in Kubernetes**

➢ ReplicationController can be used to manage the App Scaling.

➢ ReplicationController ensures that a specified number of pod replicas are running at any point of time.

➢ ReplicationController makes sure that a pod or a set of pods is always up and available.

**Demo - Scaleup and down using Replication Controller**

SSH to master node

_To create a replication controller yaml with 3 replicas and run it_

```
sudo -i
mkdir deployments
cd deployments
nano replication-controller.yaml

https://github.com/kohlidevops/DevOpsWithKubernetes/blob/main/22%20-%20ScalingApplication-ReplicationController/replication-controller.yaml

kubectl apply -f replication-controller.yaml
kubectl get replicationcontroller
or
kubectl get rc
kubect get pods -o wide
```

![image](https://github.com/user-attachments/assets/0944e69f-5a03-4d08-b89e-a3479b363ba3)

3 replicas as pods are running. What will happen if we delete any one of the pods? - It will re-create the pod.

```
kubectl delete pod <pod-name>
kubectl delete pod alipne-box-replicationcontroller-84cgf
kubectl get rc
kubect get pods -o wide
```

![image](https://github.com/user-attachments/assets/7f552bf0-977f-44af-83ea-7254b29e58fe)

_To scaleup the replicas_

Already running 3 pods, if u want to scaleup another 3 pods then you have to set replicas as 6.

```
kubectl get rc
kubectl scale --replicas=6 replicationcontroller/<replication-controller-name>
kubectl scale --replicas=6 replicationcontroller/alipne-box-replicationcontroller
kubectl get rc
kubectl get pods -o wide
```

![image](https://github.com/user-attachments/assets/ef6c0339-a0ed-4d51-ad6c-e4da58231868)

_To scaledown the replicas_

Already running 6 pods, if u want to scaledown to 2 pods then you have to set replicas as 2.

```
kubectl get rc
kubectl scale --replicas=2 replicationcontroller/<replication-controller-name>
kubectl scale --replicas=2 replicationcontroller/alipne-box-replicationcontroller
kubectl get rc
kubectl get pods -o wide
```

![image](https://github.com/user-attachments/assets/4677b107-c932-4f9e-9ca8-ef7e3bca9b96)

_Termination policy_

What will happen if you scaledown the pods? - Surely will terminate the recently launched pods.

_To delete the replication controller_

```
kubectl get rc
kubectl delete rc <controller-name>
kubectl delete rc alipne-box-replicationcontroller
kubectl get rc
```

![image](https://github.com/user-attachments/assets/29f107f0-be08-4fef-acf7-e347dfab1786)
