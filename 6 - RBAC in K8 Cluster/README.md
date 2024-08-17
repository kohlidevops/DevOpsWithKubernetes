# Role Based Access Control in Kubernetes Cluster

Kubernetes Role-Based Access Control (RBAC) is a mechanism that helps manage and restrict user access to resources within a Kubernetes cluster. 

It allows administrators to define who can access which resources and what actions they can perform on those resources.

## Roles and ClusterRoles

**Role:** Defines a set of permissions within a specific namespace. It contains rules that specify what actions can be performed on which resources.

**ClusterRole:** Similar to a Role but applies across the entire cluster, not limited to a specific namespace. It can be used for cluster-wide resources or to define global permissions.

## RoleBindings and ClusterRoleBindings:**

**RoleBinding:** Associates a Role with users, groups, or service accounts within a specific namespace. It grants the permissions defined in the Role to the specified subjects within that namespace.

**ClusterRoleBinding:** Associates a ClusterRole with users, groups, or service accounts across the entire cluster. It grants the permissions defined in the ClusterRole cluster-wide.

## Subjects:

These are the entities (users, groups, or service accounts) that are granted permissions through Roles or ClusterRoles.

## Resources and Verbs:

**Resources:** Kubernetes objects like pods, deployments, services, etc.

**Verbs:** Actions that can be performed on resources, such as get, list, create, update, delete, etc.

## Handson

**SSH to K8 cluster master node**

**1. To create a namespace**

```
sudo -i
sudo apt-get install openssl -y
kubectl get namespace
kubectl create namespace development
kubectl get namespace
```

![image](https://github.com/user-attachments/assets/673999dd-8728-41f4-95bf-16210553ed87)

**2. Create private key and a CSR (Certificate Signing Request) for DevUser**

```
cd ${HOME}/.kube
sudo openssl genrsa -out DevUser.key 2048
sudo openssl req -new -key DevUser.key -out DevUser.csr -subj "/CN=DevUser/O=development"

The common name (CN) of the subject will be used as username for authentication request. The organization field (O) will be used to indicate group membership of the user.
```

**3. Provide CA keys of Kubernetes cluster to generate the certificate**

```
sudo openssl x509 -req -in DevUser.csr -CA /etc/kubernetes/pki/ca.crt -CAkey /etc/kubernetes/pki/ca.key -CAcreateserial -out DevUser.crt -days 45
```

**4. Get Kubernetes Cluster Config**

```
kubectl config view
or
kubectl config view --flatten=true
```

**5. Add the user in the Kubeconfig file**

```
kubectl config set-credentials DevUser --client-certificate ${HOME}/.kube/DevUser.crt --client-key ${HOME}/.kube/DevUser.key
kubectl config view
//You have one more entry that use has been added
```

**6. To describe or list the kubernetes cluster name**

```
kubectl config view -o jsonpath='{.contexts[?(@.name=="'$(kubectl config current-context)'")].context.cluster}'

kubernetes
```

**7. Add a context in the config file, that will allow this user (DevUser) to access the development namespace in the cluster**

```
kubectl config set-context DevUser-context --cluster=kubernetes --namespace=development --user=DevUser
```

![image](https://github.com/user-attachments/assets/41d21848-5923-4663-afd8-0240a293bc02)

```
kubectl config view
```

![image](https://github.com/user-attachments/assets/0d03e598-29cc-428e-9a0b-d6414bff868b)

**Create a Role for the DevUser**

**1. Test access by attempting to list pods**

```
kubectl get pods --context=DevUser-context
```

![image](https://github.com/user-attachments/assets/5fb26cf1-a657-4ece-bd12-4f2312a9c677)

**2. Create a role resource using below manifest**
   
```
cd k8ObjectManagement
vi pod-reader-role.yml
//use below link to copy/paste the reader role

https://github.com/kohlidevops/DevOpsWithKubernetes/blob/main/6%20-%20RBAC%20in%20K8%20Cluster/pod-reader-role.yaml
```

**3. Create the role**

```
kubectl apply -f pod-reader-role.yml
```

![image](https://github.com/user-attachments/assets/054cb9f4-df1e-47a1-9b70-2b3ebb7e5d31)

**4. Verify Role**

```
kubectl get role -n development
```

![image](https://github.com/user-attachments/assets/61a56320-f3c6-4b2b-a8f4-f9d05496550d)

**Bind the Role to the dev User and Verify Your Setup Works**

**1. Create the RoleBinding spec file**

```
cd k8ObjectManagement
vi pod-reader-rolebinding.yaml
//copy/paste the rolebinding yaml file using below link
https://github.com/kohlidevops/DevOpsWithKubernetes/blob/main/6%20-%20RBAC%20in%20K8%20Cluster/pod-reader-rolebinding.yaml
```

**2. Create Role Binding**

```
kubectl apply -f pod-reader-rolebinding.yaml
//To get the rolebinding for particular namespace
kubectl get rolebinding -n development
```

![image](https://github.com/user-attachments/assets/1dffe122-b77b-4727-b1b8-f66ddaaff597)

**3. Test access by attempting to list pods**

```
kubectl get pods --context=DevUser-context
```

Earlier we got the error whrn get pods with DevUse-Context due to permission mising. But now it will show no pods available in this namespace So now this user group has access to this namespace.

![image](https://github.com/user-attachments/assets/62893d77-d6e6-4544-834b-c4379eeaccf6)

**4. Create Pod**

```
kubectl run nginx --image=nginx --context=DevUser-context
```

![image](https://github.com/user-attachments/assets/28b2aba4-290c-458a-8863-4da794ac9be4)

Because the pod-reader-role.yaml file has access with "get", "watch", "list", "update". Not "create". So Im going to create a nginx in development namespace as a root as Administrator

**5. Create a Pod as root user**

```
kubectl run nginx --image=nginx -n development
```

![image](https://github.com/user-attachments/assets/556ba73f-89e8-495c-a050-2dc8f24d397a)

**6. Test access by attempting to list pods**

```
kubectl get pods --context=DevUser-context
```

![image](https://github.com/user-attachments/assets/e9965ab0-eb9b-4740-ab9f-23997c76d961)

Now this particular DevUser-context can access the pod as we expected.

