# Maintenance windows Kubernetes Cluster

**Node Draining**

Node draining is the process of safely evicting all the pods from a Kubernetes node before performing maintenance on that node or removing it from the cluster.
Application shouldn't impacted by this process.

Draining Node : Containers running on that node will be gracefully terminated and re-schedule to another available node.

**Draining K8s Node**

Use Kubectl to drain node

```
kubectl drain <node_name>
```

**Ignore DaemonSet**

DaemonSets are designed to run a copy of a pod on every node in the cluster. When draining a node, you might want to keep these pods running because they are typically critical for cluster operations (like logging or monitoring). 
DaemonSet means pods that are tied to each node. If any DaemonSet is running in your K8s cluster,
use command -

```
kubectl drain <node_name> --ignore-daemonsets
```

**Uncordoning a Node**

After you’ve completed the maintenance and want to bring the node back into service, you need to mark the node as schedulable again. This is done with the kubectl uncordon command. Here’s how you use it:

```
kubectl uncordon <node-name>
```

**Cordon**

Purpose: Marks the node as unschedulable, preventing new pods from being scheduled on it.

Command: kubectl cordon <node-name>

**Uncordon**

Purpose: Marks the node as schedulable again, allowing new pods to be scheduled on it.

Command: kubectl uncordon <node-name>
  
These commands are useful for managing the availability and scheduling of nodes in your Kubernetes cluster, especially during maintenance or scaling operations.

**Demo**

Lets create a directory called nodedraining in master node and create a file called pod.yaml inside the nodedraining folder.

pods.yaml file

```
https://github.com/kohlidevops/DevOpsWithKubernetes/blob/main/3%20-%20K8%20Cluster%20-%20Maintenance%20window/pods.yaml
```

Then run this pods.yaml file on the master node

```
kubectl apply -f pods.yaml
```

![image](https://github.com/user-attachments/assets/810995fd-4799-4f9a-8af5-e3511c4c24cf)

create a deployment.yaml file inside a nodedraining folder

```
https://github.com/kohlidevops/DevOpsWithKubernetes/blob/main/3%20-%20K8%20Cluster%20-%20Maintenance%20window/deployment.yaml
```

```
kubectl apply -f deployment.yaml
kubect get nodes
kubectl get pods -o wide
```

![image](https://github.com/user-attachments/assets/ab6f65b2-e870-4f48-991f-74a58f92dd12)

**To drain the node**

```
kubectl drain <node-name>
```

![image](https://github.com/user-attachments/assets/9a248770-26a6-4187-8796-21f8a5354b56)

We are getting two errors - cannnot delete the pods are declared and cannot delete the pods which has daemons like calico proxy.

```
kubectl drain <node-name> --ignore-daemonsets
```

still getting error with pods declared For this we can run below command to evict the worker node from the k8 cluster.

```
kubectl drain <node-name> --ignore-daemonsets --force
```

Now scheduling has been disabled for one node but still it is ready state means no new resource has been schedule to this particular node.

![image](https://github.com/user-attachments/assets/558286c4-b7e9-4a0a-9ad8-32001463ae08)

If you check with list pods commands, then you can see the new pod has been reschedule in the available node.

```
kubectl get pods -o wide
```

![image](https://github.com/user-attachments/assets/791cdbde-a237-4aaf-8bef-a1a2cd57041a)

When you drain the node, the pods which are running on the particular node, they will terminate gracefully and rescheduled on the available worker node.

pods.yaml -> which are executed explictly on the worker node that is getting deleted when you drain the node.

deployment.yaml -> which are deployed by deployment file contains replicas (that replica controller is stateful). So this should be rescheduled to other available worker nodes

**To rejoin (uncordon) the worker node to the k8 cluster**

After you’ve completed the maintenance and want to bring the node back into service, you need to mark the node as schedulable again. This is done with the kubectl uncordon command

```
kubectl uncordon <node-name>
kubectl get nodes
```

![image](https://github.com/user-attachments/assets/8bda18a5-7a0a-4c97-955a-75e85c3f14c1)






