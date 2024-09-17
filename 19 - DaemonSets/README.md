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


