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

Demo

Lets create a directory called nodedraining in master node and create a file called pod.yaml inside the nodedraining folder.

pods.yaml file - 
