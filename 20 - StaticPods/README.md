# Static Pods in Kubernetes

➢ Static Pods directly managed by Kubelet on K8s Nodes.

➢ K8s API Server is not required for Static Pods.

➢ kubelet watches each static Pod (and restarts it if it fails).

➢ Kubelet automatically creates Static Pods from YAML file located at manifest path on the Node.

# Mirror Pods

➢ Kubelet will create the Mirror pod for each Static Pod.

➢ Mirror pods allows user to monitor Static Pods via K8s APIs.

➢ User can’t change or Update Static Pods via Mirror Pods.

## Demo 

_SSH to any worker node - I jump on to the worker node-02 and navigate to the manifest location._

By default, kubelet will automatically start this pod as its behavior. If it is immediately work then we can restart the kubelet service to see the magic. 

```
sudo -i
cd /etc/kubernetes/manifests/
nano static-pod.yaml

https://github.com/kohlidevops/DevOpsWithKubernetes/new/main/20%20-%20StaticPods

sudo systemctl start kubelet.service
```

_SSH to master node and you can see the mirror node_

```
sudo -i
kubectl get pods -o wide
```

![image](https://github.com/user-attachments/assets/ec411db2-811a-4b4f-bd2b-162be821b200)

_What will happen if you delete this mirror pod from control plane? It will get delete, but we cant update or delete static pods via mirror pods_

```
kubectl get pods
kubectl delete pod nginx-static-pod-ip-172-31-47-215
kubectl get pods
```

It is still running

![image](https://github.com/user-attachments/assets/e5b77dec-7e18-4b11-8a86-d1ea8f1f2e2c)

If you describe the pod, then nothing was happened in message!

![image](https://github.com/user-attachments/assets/f82a01ef-4c0f-47e6-b1a5-10c40c9388b4)
