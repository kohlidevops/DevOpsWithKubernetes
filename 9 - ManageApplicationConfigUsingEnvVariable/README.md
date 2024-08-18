# How to manage the Application configuration (ConfigMap and Secrets) using Environment variables?

## To create a ConfigMap

SSH to K8 Cluster master node

```
sudo -i
mkdir pods_and_container
cd pods_and_container
nano example-configmap.yaml
```

_Use below link to copy/paste the YAML file_

```
https://github.com/kohlidevops/DevOpsWithKubernetes/blob/main/9%20-%20ManageApplicationConfigUsingEnvVariable/example-configmap.yaml
```

_To deploy the configmap_ 

```
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
```

_Use below link to copy/paste the YAML file_

```
https://github.com/kohlidevops/DevOpsWithKubernetes/blob/main/9%20-%20ManageApplicationConfigUsingEnvVariable/example-secret.yaml
```

_To deploy the secret_

```
kubectl apply -f example-secret.yaml
kubectl get secrets
kubectl describe secret example-secret.yaml
```

![image](https://github.com/user-attachments/assets/47fd203e-762c-44f4-bdd4-a1f898deaabf)

=> When you describe configmap will expose the value

=> When you describe secret will not expose the value

=> You can delete the secret YAML file once deployed in cluster. So Kubernetes knews the value of secret. No one can access and decode the secret value

## To create a application pod

```
cd pods_and_container
nano configmap-env-demo.yaml
```

_Use below link to copy/paste the YAML file_

```
https://github.com/kohlidevops/DevOpsWithKubernetes/blob/main/9%20-%20ManageApplicationConfigUsingEnvVariable/configmap-env-demo.yaml
```

_To deploy a configmap-demo application_

```
kubectl apply -f configmap-env-demo.yaml
kubectl get pods
```

![image](https://github.com/user-attachments/assets/14c9be81-3d26-4905-941e-6dad640ced03)

To execute and ssh to configmap pod

To ssh to this pod and check the environment variable whether its mapped to configmap and secrets

```
kubectl exec <pod-name> -it -- sh
kubectl exec configmap-env-demo -it -- sh
// now logged into the container and execute below commands to check
echo $PLAYER_LIVES
echo $SECRET_USERNAME
echo $SECRET_PASSWORD
printenv
exit
```

![image](https://github.com/user-attachments/assets/24a969ff-1130-4e36-aa87-fac83d9f2d63)

This is the way we can pass the configmap and secret to the application at run time with the help of environment variables.
