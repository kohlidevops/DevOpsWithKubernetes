# Node Affinity in Kubernetes

➢ Node Affinity is enhanced version of NodeSelector.

➢ Node Affinity is used for Pods Allocation on Worker Nodes.

➢ Not to Schedule Pod on Nodes is achieve via Node Anti-Affinity. (If you dont want to schedule the pod in the particular node, then we have to go with Anti-Affinity.)

➢ Anti-Affinity is Opposite of Affinity and NodeSelector Concept.

➢ requiredDuringSchedulingIgnoredDuringExecution :

➢ requiredDuringScheduling - Must fulfil the condition at the time of Pod Creation. (Whenever the pod is scheduling in the kubernetes node, the condition whatever we are putting in a node affinity must be fulfilled. If not fulfilled then pod will not be scheduled)

➢ Also Called Hard Affinity. (Because we are force a pod to execute a particular node)

➢ IgnoredDuringExecution - Pod will still run if labels on a node change and affinity rules are no longer met.

➢ preferredDuringSchedulingIgnoredDuringExecution: 

➢ preferredDuringScheduling - (It will try to schedule the pod on a node which will justify the affinity. But if due to any reason given, it is not getting that particular node or not getting the resource on that particular node, then it will schedule the pod on some other node. So here the port creation will not be in the pending state. It will execute or schedule the port on some another node.)

➢ Also Called Soft Affinity.

## Demo - Nodeaffinity

SSH to master node

```
sudo -i
cd pods_allocation
kubectl get nodes
nano nodeaffinity.yaml

https://github.com/kohlidevops/DevOpsWithKubernetes/blob/main/21%20-%20NodeAffinity/nodeaffinity.yaml

// Clearly we mentioned in the yaml file that pod should deployed on node which has label called ssd. You can check which node has ssd label. (Here operator: In)

kubectl get nodes --show-labels
```

![image](https://github.com/user-attachments/assets/e3710df2-5c6a-4995-a67f-c1b8abcd71a6)

_To run nodeaffinity pod_

```
kubectl apply -f nodeaffinity.yaml
kubect get pods -o wide
kubectl get nodes
```

![image](https://github.com/user-attachments/assets/3212cb5a-6004-490d-983d-97addf1748de)

//Its exactly deployed on the node which node has label called "ssd"

## Demo - Node Anti-affinity

SSH to master node

```
sudo -i
cd pods_allocation
kubectl get nodes
nano nodeantiaffinity.yaml

https://github.com/kohlidevops/DevOpsWithKubernetes/blob/main/21%20-%20NodeAffinity/nodeantiaffinity.yaml

//Here we clearly mentioned the pod should be deployed which node doesn't have "ssd" label. - Because we prevent the scheduling pod on the particular node. (Here operator: NotIn)

kubectl get nodes
kubectl apply -f nodeantiaffinity.yaml
kubectl get pods -o wide
```

![image](https://github.com/user-attachments/assets/43ea4eef-c252-4715-985f-18a02793f89e)

Yes this pod has been deployed in worker node-01 which doesn't has "ssd" label.









