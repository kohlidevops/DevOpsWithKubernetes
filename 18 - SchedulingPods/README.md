# To Scheduling Pods in Kubernetes

**What is Scheduling**

➢ Scheduling is a process to assign the Pods to Nodes, so that Kubectl can run them.

➢ Scheduler : It’s a component on Kubernetes Master Node, which decide the Pods assignment on nodes.

**Scheduling Process**

➢ Kubernetes Scheduler Select the suitable node for Pods

➢ Resource Request vs Available Node Resources (If you define a resource request 4 CPU and 2 GiB memory then scheduler will allocate this pod to the worker node which meets this requirement)

➢ Configuration like Node Labels (If you define label of the node in the pod manifest yaml file, then scheduler assign this pod to the particular worker node)

➢ nodeSelector, Affinity and Anti-Affinity

**nodeSelector**

➢ nodeSelector is define in Pod Spec to limit which Node(s) the pod can be scheduled on.

➢ NodeSelector use Labels to select the suitable Node.

![image](https://github.com/user-attachments/assets/379ecc60-5905-44a2-9993-6070de39fca8)

**nodeName**

➢ User can bypass scheduling and assign Pod to a Specific Node using Node Name.

➢ NodeName is typically is not good option to use for Pod scheduling due to its limitations. (Dynamically any worker node down and new worker node will be join to the cluster)

![image](https://github.com/user-attachments/assets/e8624255-f4a1-45b5-856b-4063256bdd7e)

## Demo NodeSelector

SSH to master node and ensure both 2 workers nodes are running

```
sudo -i
mkdir pods_allocation
cd pods_allocation
nano nodeselector.yaml

https://github.com/kohlidevops/DevOpsWithKubernetes/blob/main/18%20-%20SchedulingPods/nodeselector.yaml

kubectl apply -f nodeselector.yaml
kubectl get pods -o wide
kubect describe pod nginx-nodeselector
```

![image](https://github.com/user-attachments/assets/b719a5a3-cd40-45d5-b638-1b4e4d017cb8)

Its Failed scheduling due to missed label "disktype=ssd" in any worker nodes.

_What are the labels  are attached to the cluster?_

```
kubectl get nodes --show-labels
```

![image](https://github.com/user-attachments/assets/9e2962ef-89d9-4ae7-bd28-61e946543253)

_How to assign the label to the particular worker node?_

```
kubectl label nodes ip-172-31-47-215 disktype=ssd
kubectl get nodes --show-labels
```

Here, ip-172-31-47-215 - worker node name and disktype=ssd - label

![image](https://github.com/user-attachments/assets/52c873e6-e256-4637-a80b-ed999402c73e)

Now, Failed scheduling has been successfully assigned - So pod has been is active now.

![image](https://github.com/user-attachments/assets/3efa5941-92c5-438c-88a3-ecec2285495c)

## Demo - NodeName

```
cd pods_allocation
nano nodename.yaml

https://github.com/kohlidevops/DevOpsWithKubernetes/blob/main/18%20-%20SchedulingPods/nodename.yaml

kubectl apply -f nodename.yaml
kubectl get pods -o wide
```

![image](https://github.com/user-attachments/assets/b86154ba-42b1-4231-a641-7a55553097d6)

My nodename pod has been assigned to the particular node what i mentioned in nodename yaml file.

## Demo - Resource Request

```
cd pods_allocation
nano resource-request1.yaml

https://github.com/kohlidevops/DevOpsWithKubernetes/blob/main/18%20-%20SchedulingPods/resource-request1.yaml

//Here this pod will assign to the worker node which has "disktype=ssd and mem - 64 MB & cpu - 1000m"
//disktype=ssd - This label already assigned to the worker node called ip-172-31-47-215

kubectl apply -f resource-request1.yaml
kubectl get pods -o wide
```

 ![image](https://github.com/user-attachments/assets/0e3dbdad-8695-45e7-99d8-af763e717fbe)

This pod also assigned to the same worker node.

Lets copy the same pod yaml and name it as resource-request2.yaml and run it again - whether it is assigned to the same worker node

```
nano resource-request2.yaml

https://github.com/kohlidevops/DevOpsWithKubernetes/blob/main/18%20-%20SchedulingPods/resource-request1.yaml

kubectl apply -f resource-request2.yaml
kubectl get pods -o wide
```

![image](https://github.com/user-attachments/assets/69b4f8db-4548-4460-8e24-f5152edfa8cd)

This pod is still pending. Because this pod meet first dependency that is "disktype=ssd" and it cant able to meet the cpu & mem dependency. So it cant able to assign the pod.

Let run one more pod without node selector "disktype=ssd"

```
cd pods_allocation
nano resource-request3.yaml

https://github.com/kohlidevops/DevOpsWithKubernetes/blob/main/18%20-%20SchedulingPods/resource-request2.yaml

kubectl apply -f resource-request3.yaml
kubect get pods -o wide
```

![image](https://github.com/user-attachments/assets/d333bd7d-b0c7-4f8a-8ee4-836ac0f812cd)


But this pod definetely will assign to another node. Because this yaml doesn't mention any label like "disktype=ssd".
