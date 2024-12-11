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
