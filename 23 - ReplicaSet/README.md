# ReplicaSet in Kubernetes

**Replica-Set**

➢ ReplicaSet is enhanced version of ReplicationController.

➢ Like ReplicationController, ReplicaSet's purpose is to maintain a stable set of replica Pods running at any given time.

➢ The main difference between a ReplicaSet and a ReplicationController is the selector support.

➢ Label Selectors is used to identify a set of objects in Kubernetes.

➢ ReplicaSets allow us to use “set-based” label selector.

➢ In, NotIn, Exists operators are used to Match K8s Object Labels.

**Replica-Set vs Replica-Controller**

![image](https://github.com/user-attachments/assets/6db8512b-6925-41ab-bbf1-499541fa9297)

**Bare Pods**

➢ Bare Pods are Pods created manually without a controller like a ReplicaSet or Deployment managing them.

➢ They are standalone, meaning they don't benefit from the features of controllers like automatic restart or scaling.

➢ Once they fail, they won't be automatically replaced.

➢ Labels: Bare Pods typically don't have the specific labels required for a ReplicaSet to manage them. Without matching labels, they remain unmanaged by any ReplicaSet.

**ReplicaSet**

➢ ReplicaSet ensures that a specified number of replica Pods are running at all times.

➢ It can manage Pods based on their labels.

➢ Matching Labels: A ReplicaSet uses label selectors to identify and manage Pods. It can automatically scale the number of Pods to ensure the desired state is met.
 
➢ Adopting Pods: If a Pod has labels that match the ReplicaSet's selector (even if it wasn’t originally created by the ReplicaSet), the ReplicaSet will take over management of that Pod.

## Demo - Replicaset

SSH to master and execute the replicaset pod

```
sudo -i
cd deployments
kubectl get nodes
kubectl get pods
nano replica-set.yaml

https://github.com/kohlidevops/DevOpsWithKubernetes/blob/main/23%20-%20ReplicaSet/replica-set.yaml

kubectl apply -f replica-set.yaml
kubect get rs
or
kubect get replicaset
or
kubectl get rs/myapp-replicas
kubectl get pods -o wide
kubectl describe rs/myapp-replicas
```

![image](https://github.com/user-attachments/assets/298cd465-31bd-46b3-a32d-b11118902745)

_To scaleup the replicaset_

```
kubectl get rs/myapp-replicas
kubectl get pods -o wide
kubectl get pods -o wide | grep -i myapp-replicas
kubectl scale --replicas=10 rs/myapp-replicas
kubectl get pods -o wide | grep -i myapp-replicas
```

![image](https://github.com/user-attachments/assets/a8924149-2ffd-480e-8d0e-ed4db0e6c9d9)

_To scaledown the replicaset_

```
kubectl get rs/myapp-replicas
kubectl get pods -o wide
kubectl get pods -o wide | grep -i myapp-replicas
kubectl scale --replicas=2 rs/myapp-replicas
kubectl get pods -o wide | grep -i myapp-replicas
```

![image](https://github.com/user-attachments/assets/36979f69-d51c-4b6b-a2cd-af4bf0fcd402)

