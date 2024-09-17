# Static Pods in Kubernetes

➢ Static Pods directly managed by Kubelet on K8s Nodes.

➢ K8s API Server is not required for Static Pods.

➢ kubelet watches each static Pod (and restarts it if it fails).

➢ Kubelet automatically creates Static Pods from YAML file located at manifest path on the Node.

# Mirror Pods

➢ Kubelet will create the Mirror pod for each Static Pod.

➢ Mirror pods allows user to monitor Static Pods via K8s APIs.

➢ User can’t change or Update Static Pods via Mirror Pods.
