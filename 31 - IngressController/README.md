# To Manage Access via Ingress Controller in Kubernetes

**What is an Ingress**

➢ Ingress in Kubernetes Manage the External Access to Service.

➢ Apart from NodePort Service, Ingress is capable of many more.

➢ Provide the SSL Termination, Load Balancing, NameBase Virtual Hosting.

![image](https://github.com/user-attachments/assets/507a1c65-8a5f-4dd1-8b0a-248ea0c0f91f)

**Ingress Controllers**

➢ In order for the Ingress resource to work, the cluster must have an ingress controller running.

➢ Variety of Ingress Controller available in K8s to provide the multiple mechanism for external access of Service.

➢ You can deploy any number of Ingress Controller.

➢ Ingress define a set of Routing Rules.

➢ Each Rule has a set of Paths, each with a Backend. Request matching a path will be routed to associated Backend.

![image](https://github.com/user-attachments/assets/33195417-7b3d-4b84-bc3c-30ec36323a3e)

**NamedPort**

➢ If Service Use NamedPort, ingress can also use the port’s name to choose to which port it will route.

![image](https://github.com/user-attachments/assets/f1dba130-4212-407b-9961-d7d67c291417)

## Lab - Ingress Controller

SSH to master node

_To deploy a nginx-deployment manifest file_

```
sudo -i
mkdir ingress
cd ingress
nano nginx-deployment.yaml

https://github.com/kohlidevops/DevOpsWithKubernetes/blob/main/31%20-%20IngressController/nginx-deployment.yaml

kubectl apply -f nginx-deployment.yaml
kubectl get deployment
kubectl describe deployment nginx-official-deployment
kubectl get pods -o wide
```

![image](https://github.com/user-attachments/assets/ff26a2d7-dcd5-44df-9219-199fb80eb3cb)

_To deploy a service for the deployment_

```
nano nginx-deployment-service.yaml

https://github.com/kohlidevops/DevOpsWithKubernetes/blob/main/31%20-%20IngressController/nginx-deployment-service.yaml

kubectl apply -f nginx-deployment-service.yaml
kubectl get svc
```

The nginx is now listening as 31303 port as NodePort

![image](https://github.com/user-attachments/assets/8c35f3bb-75f3-4626-b3d8-efb4c70a1dbb)

_To deploy a new deployment named magicalnginx-deployment manifest_

```
nano magicalnginx-nginx-deployment.yaml

https://github.com/kohlidevops/DevOpsWithKubernetes/blob/main/31%20-%20IngressController/magicalnginx-nginx-deployment.yaml

kubectl apply -f magicalnginx-nginx-deployment.yaml
kubectl get deployment
kubectl describe deployment magicalnginx-deployment
kubectl get pods -o wide
```

_To deploy a service for magincalnginx deployment_

```
nano magicalnginx-deployment-service.yaml

https://github.com/kohlidevops/DevOpsWithKubernetes/blob/main/31%20-%20IngressController/magicalnginx-deployment-service.yaml

kubectl apply -f magicalnginx-deployment-service.yaml
kubectl get svc
```

![image](https://github.com/user-attachments/assets/50a54880-bfd9-459d-afa0-b3c89df28002)

_To deploy a Ingress Controller for these two services_

```
nano ingress-controller.yaml

https://github.com/kohlidevops/DevOpsWithKubernetes/blob/main/31%20-%20IngressController/ingress-controller.yaml

kubectl apply -f ingress-controller.yaml
kubectl get ingress
```

![image](https://github.com/user-attachments/assets/1031f060-6d30-41fe-ad65-74f51da7bd0f)

(If you map with real domain name, then it should work)
