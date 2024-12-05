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

