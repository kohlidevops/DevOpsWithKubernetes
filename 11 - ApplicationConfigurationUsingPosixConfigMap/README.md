# How to pass sensitive information to Kubernetes application at run-time using ConfigMap Posix?

_SSH to K8 Master node_

```
sudo -i
cd pods_and_container
nano example-posix-configMap.yaml
```

**To create a configMap Posix yaml file to pass the variables and values**

_Use below link to copy/paste the yaml_

```
https://github.com/kohlidevops/DevOpsWithKubernetes/blob/main/11%20-%20ApplicationConfigurationUsingPosixConfigMap/example-posix-configMap.yaml
```

**To run the configmap posix**

```
kubectl apply -f example-posix-configMap.yaml
kubectl get configmap
```

![image](https://github.com/user-attachments/assets/dbee810f-a624-4144-b65d-cf49cbbcd7a8)

**To create a application pod for posix configmap**

```
nano configmap-posix-demo.yaml
```

_Use below link to copy/paste the application pod file_

```
https://github.com/kohlidevops/DevOpsWithKubernetes/blob/main/11%20-%20ApplicationConfigurationUsingPosixConfigMap/configmap-posix-demo.yaml
```

**To run the application pod**

```
kubectl apply -f configmap-posix-demo.yaml
kubectl get pods
kubectl describe pod configmap-posix-demo
```

![image](https://github.com/user-attachments/assets/b308440b-23b9-40f0-9673-7ced57813d18)

![image](https://github.com/user-attachments/assets/2fc3d0db-e6cc-4197-9f00-e9cf41fdfc1b)

**To logon to the container**

```
kubectl exec configmap-posix-demo -it -- /bin/bash
/#printenv
```

![image](https://github.com/user-attachments/assets/7a69393a-fc91-40a2-9e61-64df4ad31939)


