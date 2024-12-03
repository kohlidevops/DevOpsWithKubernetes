# Services in Kubernetes

## What is ServiceType

➢ Each Service has a Type. ServiceType define how and where Service will Expose the Application.

➢ There are 4 Types:

○ ClusterIP

○ NodePort

○ LoadBalancer

○ ExternalName

## ClusterIP Service

➢ ClusterIP Service expose Application within Cluster Network.

➢ Use ClusterIP, when client is Other Pods within the Cluster.

![image](https://github.com/user-attachments/assets/60da70dd-3614-449e-8f5a-25146f95dd1a)

## NodePort Service

➢ NodePort Service expose Application Outside Cluster Network.

➢ Use NodePort, when client is accessing the Service from Outside the Cluster.

![image](https://github.com/user-attachments/assets/9367b21c-1516-4450-9973-66baa82778bf)

## LoadBalancer Service

➢ Load Balancer Service also expose Application to Outer World but Cloud LB is required.

![image](https://github.com/user-attachments/assets/fc07747c-52a7-4981-9168-64134e6df5cd)

## Demo - Service

### Service - ClusterIP

SSH to master node and create a directory named k8Service

_To create a deployment manifest file_

```
sudo -i
kubectl get nodes
mkdir k8Service
cd k8Service
nano deployment.yaml

https://github.com/kohlidevops/DevOpsWithKubernetes/blob/main/29%20-%20Services/deployment.yaml

kubectl apply -f deployment.yaml
kubectl get pods -o wide
```

![image](https://github.com/user-attachments/assets/1f9dbeb7-6980-4607-af6d-44ec48aadd5a)

_To create clusterIp yaml _

```
nano  clusterip-service.yaml

https://github.com/kohlidevops/DevOpsWithKubernetes/blob/main/29%20-%20Services/clusterIp-service.yaml

kubectl apply -f clusterip-service.yaml
kubectl get svc
kubectl describe svc <service-name>
kubectl describe svc nginx-service
curl nginx-service:8080
```

![image](https://github.com/user-attachments/assets/c84a25db-fbdb-4cf3-8f43-06533e457f3f)

If you try to access the service with port

![image](https://github.com/user-attachments/assets/b5622042-54cb-43e3-b30b-cdeeaa442ca8)


