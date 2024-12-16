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

SSH to master node and create a localhost-sc

```
sudo -i
cd k8_storage
nano localhost-sc.yaml

https://github.com/kohlidevops/DevOpsWithKubernetes/blob/main/33%20-%20PersistentVolume/localhost-sc.yaml

kubectl apply -f localhost-sc.yaml
kubectl describe storageclass.storage.k8s.io/local-storage
```

![image](https://github.com/user-attachments/assets/46af507c-dd0e-4317-a56a-2e62fbb8a007)

_To create a PV_

```
cd k8_storage
nano my-persistent-volume.yaml

https://github.com/kohlidevops/DevOpsWithKubernetes/blob/main/33%20-%20PersistentVolume/my-persistent-volume.yaml

kubectl apply -f my-persistent-volume.yaml
kubectl describe persistentvolume/my-persistnt-vol
```

![image](https://github.com/user-attachments/assets/91f09f32-3f8a-42b9-a5c3-cc8879dc8262)

_To create a PVC_

```
cd k8_storage
nano my-pvc.yaml

https://github.com/kohlidevops/DevOpsWithKubernetes/blob/main/33%20-%20PersistentVolume/my-pvc.yaml

kubectl apply -f my-pvc.yaml
kubectl describe persistentvolumeclaim/my-pvc
```

![image](https://github.com/user-attachments/assets/2d012440-1533-4f90-9b97-d7ffd2c5e9fb)

_To check the pv and pvc state_

```
kubectl get pv -o wide
kubectl get pvc -o wide
```

![image](https://github.com/user-attachments/assets/880725ac-b36e-4474-ba52-a3bb652b021f)

_To create a Pod_

```
nano my-pv-pod.yaml

https://github.com/kohlidevops/DevOpsWithKubernetes/blob/main/33%20-%20PersistentVolume/my-pv-pod.yaml

kubectl apply -f my-pv-pod.yaml
kubectl get pv -o wide
kubectl get pvc -o wide
```

![image](https://github.com/user-attachments/assets/13cf73d5-6604-4ad2-bed3-0692fd9e6c4c)

_To check in the worker node_

```
sudo -i
ls -lh /var/tmp
cat /var/tmp/success.txt
```

![image](https://github.com/user-attachments/assets/bc00523f-fa59-4859-918f-194e3169c8ca)

