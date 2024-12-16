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
