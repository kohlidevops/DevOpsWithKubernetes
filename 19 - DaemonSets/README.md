# Daemonsets in Kubernetes

➢ Automatically Run a copy of a Pod on Each Node.

➢ DaemonSet run a Copy of a Pod on New Node as they added to Cluster.

➢ DaemonSet will be helpful in case of Monitoring, Log Collection, Proxy Configuration etc.

➢ If Pods are normally not scheduled on a node due to node labels, taints, or unschedulable states, DaemonSet will not create a Pod on that node.

## Demo - Daemonsets in Kubernetes

SSH to master node

```
sudo -i
cd pods_allocation
kubectl get nodes
kubectl get pods
```

2 worker nodes are running and no pods are running as of now

![image](https://github.com/user-attachments/assets/821dd3ed-4eec-465a-85c8-7da21d931200)

_To create a daemonset yaml file_

```
https://github.com/kohlidevops/DevOpsWithKubernetes/blob/main/19%20-%20DaemonSets/daemonset.yaml
```

_To run the daemonset_

```
kubectl apply -f daemonset.yaml
kubectl get pods -o wide
```

![image](https://github.com/user-attachments/assets/962da154-f367-435f-b4fd-c06ed34d63b2)

As it is, this daemonset pod are deployed in all the nodes than control plane.

Why not in controlplane? - By default, Kubernetes applies a taint to control plane nodes to prevent scheduling regular workloads, including DaemonSet pods.

_What will happen If selector doesnot match the template labels when dameonset pod create?_ 

It wont create and threw the error.

_To delete the running daemonsets using below command_s

```
kubectl get daemonset
kubectl delete daemonset <daemonset-name>
kubectl delete daemonset logging
kubectl get pods -o wide
```

_To run the one more daemonset yaml file with mismatch label_

```
nano daemonset-1.yaml

https://github.com/kohlidevops/DevOpsWithKubernetes/blob/main/19%20-%20DaemonSets/daemonset-1.yaml

kubectl apply -f daemonset-1.yaml
kubectl get pods -o wide
```

![image](https://github.com/user-attachments/assets/ceae75a7-1ec9-4dc1-a003-fa4f80f2b45d)



