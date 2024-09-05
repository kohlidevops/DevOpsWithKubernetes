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

