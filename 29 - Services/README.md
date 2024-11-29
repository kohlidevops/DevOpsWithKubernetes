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
