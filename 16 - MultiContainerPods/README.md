# Kubernetes - Multi Container in single Pods

**Multi Container Pods**

➢ Kubernetes Pods can have Single or Multiple Containers.

➢ In Multi Container Pods, containers share the resources like network and storage, also can communicate on Local Host.

➢ Note: Best Practice is to keep the containers in separate Pods, until we would like containers will share the resources.

**Cross Container Communication**

➢ Container sharing a Pod, can interact with Shared resources.

➢ Network : Containers share the same Network and communicate on any Port, unless the port is exposed to cluster.

➢ Storage : Containers Can use shared Volume to share the data in a Pod.

**Demo - Multi Container in Single Pods**

SSH to master node

_Let's run the single container_

```
sudo -i
cd pods_and_container
nano single-container.yaml

https://github.com/kohlidevops/DevOpsWithKubernetes/blob/main/16%20-%20MultiContainerPods/single-container.yaml

kubectl get pods -o wide
kubectl exec -it two-containers -- curl http://192.168.243.146:80
```

Now you can see the forbidden message as below

![image](https://github.com/user-attachments/assets/d2a690f5-8bc4-4815-be2d-552ebb744768)

Remove the single container and run the multi-container pod again

_Let's run the multi container_

```
nano multi-container.yaml

https://github.com/kohlidevops/DevOpsWithKubernetes/blob/main/16%20-%20MultiContainerPods/multi-container.yaml

kubectl apply -f mult-container.yaml
kubectl exec -it two-containers -- curl http://192.168.243.145:80
```

![image](https://github.com/user-attachments/assets/c76ad399-a7e0-44b2-b7ce-a15d63bf50fa)

Now I can able to access. Because after the multi-container the volume has been shared. second container mounted volume has the custom index.html
