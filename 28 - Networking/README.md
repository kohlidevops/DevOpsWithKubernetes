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

## Network Policy Components

➢ podSelector : Determines to which Pods in namespace the NetworkPolicy will be applied.

➢ podSelector can select the Pods using Labels.

➢ An empty podSelector selects all pods in the namespace.

## Network Policy Components

➢ Network Policy apply on Ingress, Egress and Both kind of Traffic.

➢ Ingress : Incoming Network Traffic coming into the Pod from another Source.

➢ Egress : Outgoing Network Traffic that leaving the Pod for another Destination.

## To and From Selector - podSelector

➢ fromSelector : Selects Ingress Traffic that will be allowed on Pods.

➢ toSelector : Selects Egress Traffic that will be allowed from Pods

![image](https://github.com/user-attachments/assets/bfc594a3-514b-46d1-888c-c1d0bb2d543b)

## To and From Selector - namespaceSelector

![image](https://github.com/user-attachments/assets/70389a28-bab4-49f1-bbe9-ceaf3cdee16d)

## To and From Selector - ipBlock

![image](https://github.com/user-attachments/assets/4899738f-adb6-4d64-a558-f07a7a58afb4)

## Ports in Network Policy

![image](https://github.com/user-attachments/assets/7723b0bc-eb6e-402d-9388-7075aec3dbea)

## Demo - Network Policies

SSH to master node and execute below commands

```
sudo -i
mkdir network_policy
cd network_policy
kubectl get nodes
kubectl get ns
```

![image](https://github.com/user-attachments/assets/f64a1e47-f7f0-4039-9b44-e04608ca9eba)

_To create a new namespace and add new label to the namespace_

```
kubectl create namespace network-policy
kubectl get ns
kubectl get ns --show-labels
kubectl label namespace network-policy role=test-network-policy
kubectl get ns --show-labels
```

![image](https://github.com/user-attachments/assets/1a2c02de-0706-4835-83df-63c8d8e95eaa)

To deploy a network policy pod yaml

```
nano network-policy-pod.yaml

https://github.com/kohlidevops/DevOpsWithKubernetes/blob/main/28%20-%20Networking/network-policy-pod.yaml

kubectl apply -f network-policy-pod.yaml
kubectl get pods -o wide -n network-policy
```

![image](https://github.com/user-attachments/assets/0b3f9c4c-9c9e-4ccb-978c-6a833da611ae)

There are two pods running and try to access the nginx-pod from busybox-pod

```
kubectl exec -n network-policy busybox-pod -- curl <nginx-pod ip address>
kubectl exec -n network-policy busybox-pod -- curl 192.168.243.186
```

we can access it. We still not apply any network policy means there is no port restriction and pods are non-isolated.

![image](https://github.com/user-attachments/assets/6592e088-ea2a-4aae-b21a-f2a6be1cf9da)

To create network policy and try to access the nginx pod

```
nano network-policy.yaml

https://github.com/kohlidevops/DevOpsWithKubernetes/blob/main/28%20-%20Networking/network-policy.yaml

kubectl apply -f network-policy.yaml
kubectl get networkpolicy -n network-policy -o wide
kubectl exec -n network-policy busybox-pod -- curl 192.168.243.186
```

![image](https://github.com/user-attachments/assets/899adc55-c146-4f94-9343-5c9dffaed2d8)

We cant able to access the nginx pod from busy box. Because the we applied network policies, but not mentioned any ingress or egress rule. Now add the ingress rules in the same file using execute commands below and access the pod.

```
nano network-policy.yaml

https://github.com/kohlidevops/DevOpsWithKubernetes/blob/main/28%20-%20Networking/network-policy1.yaml

kubectl apply -f network-policy.yaml
kubectl get networkpolicy -n network-policy -o wide
kubectl exec -n network-policy busybox-pod -- curl 192.168.243.186
```

![image](https://github.com/user-attachments/assets/2cbe7f99-ea24-4883-be8e-cafeffdeb25a)

Now I can able to access the pod. Because namespace selector and port added for exact namespace.
