# Container Initialisation in Kubernetes

**Init Containers**

➢ Init Containers are specialized containers that run before app containers in a Pod.

➢ Init Container only run once during the start-up process of Pod.

➢ Init containers can contain utilities or setup scripts not present in an app image.

➢ User Can define N Number of Init Container in Pod.

![image](https://github.com/user-attachments/assets/6620dc04-36c0-4025-b62e-d665310d45e6)

**Init Containers: Use Case**

➢ SetUp the Application Init or SetUp Scripts.

➢ Init containers offer a mechanism to block or delay app container startup until a set of preconditions are met.

➢ Init containers can securely run utilities or custom code that would otherwise make an app container image less secure.

➢ Populate Data at Shared Volume before Application StartUp.

## Demo - Init Container

SSH to master node

```
sudo -i
cd pods_and_container
nano init-container.yaml

https://github.com/kohlidevops/DevOpsWithKubernetes/blob/main/17%20-%20ContainerInitialisation/init-container.yaml

kubectl apply -f init-container.yaml
kubect get pods -o wide
kubectl logs example-pod -c main-app
```

![image](https://github.com/user-attachments/assets/2426fc71-fac3-458a-9f9c-b09c06b62c35)

