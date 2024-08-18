# How to pass the ConfigMaps and Secrets to the Application at run time using mount volumes?

SSH to K8 Cluster master node

```
sudo -i
cd pods_and_container
```

Already we have a configmap and secret yaml file. Create if doesn't exist

```
https://github.com/kohlidevops/DevOpsWithKubernetes/blob/main/9%20-%20ManageApplicationConfigUsingEnvVariable/example-configmap.yaml

https://github.com/kohlidevops/DevOpsWithKubernetes/blob/main/9%20-%20ManageApplicationConfigUsingEnvVariable/example-secret.yaml
```

To create a yaml file for mount volume

```
cd pods_and_container
nano configmap-vol-demo.yaml
