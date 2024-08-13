# Kubernetes Cluster Management

![image](https://github.com/user-attachments/assets/9073204d-4e9b-4458-a915-8fb089c8b11e)


![image](https://github.com/user-attachments/assets/0fdf4cf2-1c76-4bcd-bb21-5814962f5858)


![image](https://github.com/user-attachments/assets/f167551f-ffaf-44ab-99c5-46c8fe4b82cf)


![image](https://github.com/user-attachments/assets/eca6a372-326f-4a37-9116-0471f0ac63e5)


![image](https://github.com/user-attachments/assets/1680e2e7-ac90-463c-b0dc-cf4e84e115c0)


### Stacked etcd

In a stacked etcd topology, the etcd members run on the same nodes as the Kubernetes control plane components (like kube-apiserver, kube-controller-manager, and kube-scheduler). This means that the etcd nodes and control plane nodes are in the same node.

### External etcd

In an external etcd topology, the etcd members run on separate nodes, independent of the Kubernetes control plane nodes. The etcd cluster is decoupled from the control plane, often running on dedicated machines.

