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
