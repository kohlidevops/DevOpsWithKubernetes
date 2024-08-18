# How to manage the Application configuration (ConfigMap and Secrets) using Environment variables?

## To create a ConfigMap

SSH to K8 Cluster master node

```
sudo -i
mkdir pods_and_container
cd pods_and_container
nano example-configmap.yaml
// use below link to copy/paste the YAML file
https://github.com/kohlidevops/DevOpsWithKubernetes/blob/main/9%20-%20ManageApplicationConfigUsingEnvVariable/example-configmap.yaml
kubectl apply -f example-configmap.yaml
kubectl get configmaps
kubectl describe configmap player-pro-demo
```

![image](https://github.com/user-attachments/assets/47ec7ff7-0102-438e-9314-d87e86964c66)

![image](https://github.com/user-attachments/assets/e70cba9d-f21b-4c4a-8a75-ed675171baf4)

## To create a secret

```
cd pods_and_container
nano example-secret.yaml
// use below link to copy/paste the YAML file
https://github.com/kohlidevops/DevOpsWithKubernetes/blob/main/9%20-%20ManageApplicationConfigUsingEnvVariable/example-secret.yaml
kubectl apply -f example-secret.yaml
kubectl get secrets
kubectl describe secret example-secret.yaml
```

![image](https://github.com/user-attachments/assets/47fd203e-762c-44f4-bdd4-a1f898deaabf)

=> When you describe configmap will expose the value

=> When you describe secret will not expose the value

=> You can delete the secret YAML file once deployed in cluster. So Kubernetes knews the value of secret. No one can access and decode the secret value

## To create a 

```

https://github.com/kohlidevops/DevOpsWithKubernetes/blob/main/9%20-%20ManageApplicationConfigUsingEnvVariable/configmap-env-demo.yaml
```
