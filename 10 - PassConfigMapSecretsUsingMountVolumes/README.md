# How to pass the ConfigMaps and Secrets to the Application at run time using mount volumes?

_SSH to K8 Cluster master node_

```
sudo -i
cd pods_and_container
```

_Already we have a configmap and secret yaml file. Create if doesn't exist_

```
https://github.com/kohlidevops/DevOpsWithKubernetes/blob/main/10%20-%20PassConfigMapSecretsUsingMountVolumes/example-configmap.yaml
https://github.com/kohlidevops/DevOpsWithKubernetes/blob/main/10%20-%20PassConfigMapSecretsUsingMountVolumes/example-secret.yaml
```

**To create a yaml file for mount volume**

```
cd pods_and_container
nano configmap-vol-demo.yaml
```

_Use below link to copy/paste the yaml file_

```
https://github.com/kohlidevops/DevOpsWithKubernetes/blob/main/10%20-%20PassConfigMapSecretsUsingMountVolumes/configmap-vol-demo.yaml
```

**To deploy a application pod with mount volume**

```
kubectl apply -f configmap-vol-demo.yaml
kubectl get pods
```

_To ssh the pod and check the mount volume_

```
kubectl exec <pod-name> -it -- sh
kubectl exec configmap-vol-demo -it -- sh
/#
/#ls /etc/config/configMap/
/#ls /etc/config/secret/
/#cat /etc/config/configMap/player_lives
/#cat /etc/config/secret/username
/#/etc/config/secret/password
/#exit
```

![image](https://github.com/user-attachments/assets/420b9fb0-0a12-4c3c-8598-3520ff66a442)

This is the way we can pass the configmap and secrets to the application at run-time using mount volume

