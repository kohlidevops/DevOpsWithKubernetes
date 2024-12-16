# Persistent Volume in Kubernetes

## Persistent Volume

➢ PersistentVolumes are k8s Object that allow user to treat Storage as an Abstract Resource.

➢ PV is resource in the cluster just like a node is a cluster resource.

➢ PV uses a set of Attribute to describe the underlying storage resources (Disk or Cloud Storage), which will be used to store data.

## Storage Class

➢ Admin cloud create a StorageClass called Slow to describe inexpensive storage for general Development use.

➢ Admin cloud create a StorageClass called Fast for High I/O Operation Applications.

## allowVolume Expansion

➢ allowVolumeExpansion - This field can accept boolean value only.

➢ This is the property of StorageClass and define whether StorageClass supports the ability to resize after they are created.

➢ All Cloud Disk Supports this property.

## Reclaim Policy

➢ persistentVolumeReclaimPolicy - This define, how the storage will be reused, when the PVs associated PVCs are deleted.

➢ Retain - Keep all the data. This require manual data cleanup and prepare for reuse.

➢ Delete - Delete underlying storage resources automatically (Support for Cloud Resource Only).

➢ Recycle - Automatically delete all data in underlying storage. Allow PVs to be reuse.

## PersistentVolumeClaim

➢ PersistentVolumeClaim (PVC) is a request for storage by a user.

➢ PVCs define a set of attribute Similar to those of PVs.

➢ PVCs look for a PVs that is able to meet the criteria. If it found one, will automatically be bound to that PV.

## Lab - Persistent Volume
