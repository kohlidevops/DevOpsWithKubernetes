# Kubernetes Storage

## Container File System

➢ Container File System is ephemeral.

➢ Files in container File System Exists only as long as the Container Exists.

➢ Data in container File System is lost as soon as Container Deleted or recreated.

## Volumes

➢ Many Application needs a persistent Data.

➢ Volumes allows to store Data Outside the Container, while allow container to Access Data at RunTime

## Persistent Volumes

➢ Volumes offer a way to provide external storage to container within the Pod/Container Specification.

➢ Persistent Volumes are a bit more advanced than Volumes.

➢ Persistent Volumes allow user to treat Storage as an Abstract Resource and consume it using Pods.

![image](https://github.com/user-attachments/assets/18472f72-cb1e-47f5-b188-5bc78f102c7c)


## Volume Types

➢ Volume & Persistent Volumes each have a Volume Type.

➢ Volume Type determines how storage will be handled.

➢ Various Volume Types supposts in K8s:

○ NFS - Network file System

○ Cloud Storage - AWS, GCP, Azure

○ ConfigMaps & Secrets

○ File System on K8s Node

## Volumes & Volume Mount

➢ Volume : In Pod Spec, user can define the storage volume available in for the Pod.

➢ Volume Specify the VolumeType and where the data is actually store.

➢ VolumeMount : VolumeMount in container spec, refer the Volume in Pod Spec and provide a MountPath.

![image](https://github.com/user-attachments/assets/d2661f72-c028-4578-86f5-2e166c75f3fb)

## emptyDir Volume

➢ emptyDir : emptyDir created when Pod is assigned to Node and Persist as long as Pod running on the Node.

➢ Multiple containers can refer the same emptyDir Volume.

➢ Multiple containers in the Pod can read and write the same files in the emptyDir volume, though that volume can be mounted at the same or different paths in each container.

![image](https://github.com/user-attachments/assets/b3c0d9aa-6e55-40e6-a576-c76aeea9f675)

## Share Volume

➢ User can use the same volumeMounts to share the same Volume to multiple container within the Same Pod.

➢ This is very powerful feature which can be used to data transformation of Data Processing.

➢ hostPath & emtpyDir volumeType support share volumes.

![image](https://github.com/user-attachments/assets/f109e270-a767-4b40-8d15-518a998131c6)


## Lab - Host Path

_SSH to master node_

```
sudo -i
kubectl get nodes
mkdir k8_storage
cd k8_storage
nano hostpath-volume-mount.yaml

https://github.com/kohlidevops/DevOpsWithKubernetes/blob/main/32%20-%20Storage/hostpath-volume-mount.yaml

kubectl apply -f hostpath-volume-mount.yaml
```

_SSH to worker node_

```
sudo -i
ls -lh /var/tmp/
cat /var/tmp/output.txt
```

![image](https://github.com/user-attachments/assets/03ea91bd-e1b9-4233-86f4-a931c27c2700)

_Even if u delete the pod, the data is available in worker node. If you create a pod again then this pod will use the same volume._

![image](https://github.com/user-attachments/assets/a4e4b208-fffc-4766-83dd-a4857b73c3e3)

![image](https://github.com/user-attachments/assets/b89550fa-c78f-450b-bf06-b11e1ddc4a3c)


## Lab - EmptyDir

SSh to master node

```
sudo -i
nano emptyDir-volume.yaml

https://github.com/kohlidevops/DevOpsWithKubernetes/blob/main/32%20-%20Storage/emptyDir-volume.yaml

kubectl apply -f emptyDir-volume.yaml
kubectl get pods -o wide
```

![image](https://github.com/user-attachments/assets/2250a8c1-b209-40a0-a2d7-febc059d7d22)

SSH to container

```
kubectl exec -it <pod-name> -- /bin/bash
ls -lh /data/redis/
cd /data/redis/
touch f1 f2
exit
```

![image](https://github.com/user-attachments/assets/170e355f-d518-4ce9-b6d7-4270fb714ae2)

Now delete the pod and recreate the pod and check the volume and file if its available or not

```
kubectl delete -f emptyDir-volume.yaml
kubectl apply -f emptyDir-volume.yaml
kubectl exec -it <pod-name> -- /bin/bash
ls -lh /data/redis/
cd /data/redis/
ls
```

_Files are missing - Becuase when the pod is deleted then emptyDir volume should delete Whereas if container is deleted or restarted the files are exisit.

If container deleted or restarted, then files should be exist

If pod is deleted then files should not be exist_

![image](https://github.com/user-attachments/assets/fbaec520-e72a-4641-9da7-a788c6e46af3)

