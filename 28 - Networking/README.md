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

## Network Policy

_Traffic Flow Control:_

Network policies regulate both ingress (incoming) and egress (outgoing) traffic, defining which Pods or external IP addresses are allowed to send or receive traffic from the targeted Pods.

_K8s Object:_

A Network Policy is a first-class Kubernetes object that defines rules regarding the allowed network communication to/from Pods.

_Identifiers for Pod Communication:_

Pod Selector: You can control traffic based on labels assigned to Pods. This allows traffic only from or to specific Pods with matching labels.

Namespace Selector: Network policies can also restrict traffic based on namespaces. This means you can permit or deny traffic between Pods across different namespaces.

IP Block: This allows for more granular control, enabling or restricting traffic to specific CIDR IP ranges, useful when defining external IP ranges allowed to interact with Pods.

**What is Network Policy**

➢ Network policies allows to Build a secure network by keeping Pods Isolated from traffic they do not need.

➢ By default, pods are non-isolated; they accept traffic from any source.

➢ Pods become isolated by having a NetworkPolicy that selects them.


