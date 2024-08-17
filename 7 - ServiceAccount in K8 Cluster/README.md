# Service Accounts in Kubernetes Cluster

## How can we create a Service Account and how can we create a Rolebinding for Service Account?

##### continue of below topic
```
https://github.com/kohlidevops/DevOpsWithKubernetes/tree/main/6%20-%20RBAC%20in%20K8%20Cluster
```

**1. To create a Service Account in K8 cluster master node**

SSH to master node

```
sudo -i
cd k8ObjectManagement
nano myserviceaccount.yaml
//copy/paste the below content using link

https://github.com/kohlidevops/DevOpsWithKubernetes/blob/main/7%20-%20ServiceAccount%20in%20K8%20Cluster/my-serviceaccount.yaml

kubectl get serviceaccounts
kubectl get serviceaccounts -n development
kubectl get serviceaccounts -n kube-system

kubectl apply -f my-serviceaccount.yaml
```

![image](https://github.com/user-attachments/assets/4e44024f-b02e-435a-bc5e-9ae952f29319)

**2. To list the service account with specific namespace**

```
kubectl get serviceaccounts -n development
```

![image](https://github.com/user-attachments/assets/a891c859-ec27-408b-a8a7-ec784780dffd)

**3. To create a service account binding with role**

```
kubectl get roles -n development

nano service-account-binding.yaml
//copy/paste the content using below link
https://github.com/kohlidevops/DevOpsWithKubernetes/blob/main/7%20-%20ServiceAccount%20in%20K8%20Cluster/service-account-binding.yaml

kubectl aaply -f service-account-binding.yaml
```

![image](https://github.com/user-attachments/assets/bcec1316-7311-4ed3-b0b4-8268c977bfb7)

**4. To get the rolebinding for specific namespace**

```
kubectl get rolebinding -n namespace
```

![image](https://github.com/user-attachments/assets/407234ea-11c4-4c8d-a8f1-3bc7893ed906)

