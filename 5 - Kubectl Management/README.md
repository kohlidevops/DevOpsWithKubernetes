# Kubectl Management

**kubectl**

Kubectl is command line tool for Kubernetes.

Kubectl uses the K8s APIs internally to carryout the commands.

**kubectl get**

Kubectl get is used to get the objects, present in K8s Cluster

```
$ kubectl get <object_type> <object_name> -o <output> —sort-by <JSONpath> —selector <selector>

-o — Set Output format YML/JSON
-sort-by — Sort Output using JSON path Expression
-Selector — Filter results by label
```

**kubectl describe**

You can get Detailed Information about any Kubernetes Object.

```
kubectl describe <object_type> <object_name>
```

**kubectl create**

You can create any K8s Object using Kubectl create.

File descriptor must be YAML.

```
kubectl create -f <file_name>
```

**kubectl apply**

Kubectl apply is similar to Kubectl create.

If user use kubectl apply on already existing object. It will modify the existing object, if possible.

```
kubectl apply -f <file_name>
```

**kubectl create vs kubectl apply**

kubectl create - This command will create the resources defined in deployment.yaml. If the deployment already exists, the command will fail.

kubectl apply - This command will create the resources defined in deployment.yaml if they don’t exist, or update them if they already exist.

**kubectl delete**

Kubectl delete, deletes the object from K8s Cluster.

```
kubectl delete <object_type> <object_name>
```

**kubectl exec**

Kubectl exec, used to run commands inside container.

K8s resource must be running on which kubectl exec is being performed.

```
kubectl exec <pod_name> -c <conatiner_name>
```

**Handson**

SSH to Master node

```
sudo -i
kubectl get nodes
```

![image](https://github.com/user-attachments/assets/5a08d24b-8faf-4675-9f70-db59d2b92210)

**To create a object**

```
mkdir k8ObjectManagement
cd k8ObjectManagement
nano pods.yaml

https://github.com/kohlidevops/DevOpsWithKubernetes/blob/main/3%20-%20K8%20Cluster%20-%20Maintenance%20window/pods.yaml

save and exit
kubectl create -f pods.yaml
```

![image](https://github.com/user-attachments/assets/b93ca830-cc6c-4cbc-b686-95953884d5a2)

**How many objects can support by kubernetes**

```
kubectl api-resources | wc -l
```
**To list the pods which are running in the namespace called kube-system**

```
kubectl get pods -n kube-system
```

![image](https://github.com/user-attachments/assets/40fe930f-139c-4b0e-9a41-7cbe92b2394c)

**To define or show the information about the particular pod**

```
kubectl get pods draining-node-test-pod -o wide
```

![image](https://github.com/user-attachments/assets/250740f1-a637-4ae2-bb91-6af4d31dbd3b)

**To define or show the information about the particular pod as json format**

```
kubectl get pods draining-node-test-pod -o json
```

![image](https://github.com/user-attachments/assets/1498e5eb-c295-4062-bd22-40626e946e7c)

**To define or show the information about the particular pod as json format**

```
kubectl get pods draining-node-test-pod -o yaml
```

![image](https://github.com/user-attachments/assets/0e2a6085-36b8-4476-aacd-6781211e25a9)

**To describe the pods**

```
kubectl describe pods draining-node-test-pod
```

![image](https://github.com/user-attachments/assets/32b335ac-9753-4ce7-a648-0ccc86d975c6)

**To get the container name of your pod**

```
kubectl get pod draining-node-test-pod -o jsonpath='{.spec.containers[*].name}'
```

**To execute a commands in a container running in a k8 pods**

kubectl exec is a command used to execute a command in a container running in a Kubernetes pod. It’s particularly useful for debugging or inspecting the state of a container.

```
kubectl exec <pod-name> -c <container-name> -- cat /etc/nginx/nginx.conf
kubectl exec draining-node-test-pod -c nginx -- cat /etc/nginx/nginx.conf
```

**To delete the pods**

```
kubectl delete pods draining-node-test-pod
kubectl get pods
```
