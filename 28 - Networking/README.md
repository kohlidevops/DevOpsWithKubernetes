# Networking in Kubernetes

➢ Kubernetes Network define how networking behave between Pods.

➢ Many Network Implementation available in Kubernetes.

➢ We are Using Calico Network in K8s HA SetUp.

➢ Kubernetes imposes the following fundamental requirements on any networking implementation.

```
Pods on a node can communicate with all Pods on all nodes without NAT.
Agents on a node (e.g. system daemons, kubelet) can communicate with all pods on that node.
Every Pod gets its own IP address.
```

## CNI Plugins

➢ CNI PlugIns are Kubernetes Network PlugIns.

➢ CNI PlugIns provide connectivity between Pods as per K8s Network Model.

➢ Multiple CNI Network PlugIns available.

➢ Selection of CNI PlugIn depends on your Business Needs.

➢ Our HA SetUp, we used Calico Network PlugIn. (Calico is the best one for kubeadm)

➢ K8s Nodes will remain NotReady until you install Network Plugin. And user won’t be able to Run Pods.


