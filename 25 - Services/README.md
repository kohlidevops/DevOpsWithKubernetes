# Services in Kubernetes

➤ Service is used to Access the Application Running on Pods.

➤ Pods are Dynamic in Kubernetes, Pods created and terminated on Demand.

➤ Using Replication Controller, Pods are created and Terminated during the Scaling.

➤ Using Deployments, Pods are Terminated and new Pods are take place during the Image Version Upgrade.

➤ Pod’s can’t be accessed directly, but thru a Service.

➤ Kubectl Expose command created a Service for Pods so that they can be accessible Externally.

➤ Creating a Service will create and End-Point for Pods.

➤ The set of Pods targeted by a Service is usually determined by a selector in manifest file.

➤ Publish Service, Service Type.

➤ ClusterIP: Exposes the Service on a cluster-internal IP. Choosing this value makes the Service only reachable from within the cluster.

➤ NodePort: Exposes the Service on each Node’s IP at a static port. You’ll be able to contact the NodePort Service, from outside the cluster, by requesting <NodeID>:<NodePort>

➤ Load Balancer: Exposes the Service externally using a cloud provider’s load balancer. NodePort and ClusterIP Services, to which the external load balancer routes, are automatically created.

➤ External Name : Maps the Service to the contents of the external name field, by returning a CNAME record.

## Lab - Services in Kubernetes

_To create a pod manifest file_

SSH to master

```
sudo -i
kubect get nodes
mkdir service
cd service
nano pod-manifest.yaml

https://github.com/kohlidevops/DevOpsWithKubernetes/blob/main/25%20-%20Services/pod-manifest.yaml

kubectl apply -f pod-manifest.yaml
kubect get pods
```

![image](https://github.com/user-attachments/assets/c5a0bcd9-e3c3-4a1a-8480-d960e6ccf1fd)

_To create a service manifest file_

```
cd service
nano pod-service.yaml

https://github.com/kohlidevops/DevOpsWithKubernetes/blob/main/25%20-%20Services/pod-service.yaml

kubect apply -f pod-service.yaml
kubect get service
or
kubect get svc
kubectl describe service nginx-service
```

![image](https://github.com/user-attachments/assets/36804eba-9032-4324-8186-c7b00c6ec7d0)

You can access the nginx page with EC2 instance publicip:31010

![image](https://github.com/user-attachments/assets/311bdcb8-95c9-48b0-8f2a-28aabdf39d13)

_To delete a service_

```
kubect get svc
kubectl delete service <service-name>
kubectl delete service nginx-service
```
