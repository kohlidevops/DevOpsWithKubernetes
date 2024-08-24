# To Create a ConfigMap and Secret From a File

SSH to the K8 Master node

```
sudo -i
cd pods_and_container
```

**To update and install the apache2 in master node**

```
apt-get update -y
apt-get install apache2-utils -y
```

**To create a htpasswd file**

```
htpasswd -c .htpasswd user
:Enter password
ls -lah
```

htpasswd file has been created

![image](https://github.com/user-attachments/assets/2bee3c99-0c53-4ff1-9505-357d33647deb)

**To view the htpasswd file**

```
cat .htpasswd
//You can see the username and the encrypted password
```

![image](https://github.com/user-attachments/assets/d3e1856d-af0b-4335-85bb-cf25ef35f167)

To create a secret and read from a .htpasswd file

```
kubectl create secret generic nginx-htpasswd --from-file .htpasswd
kubectl get secrets
kubectl describe secrets nginx-htpasswd
```

![image](https://github.com/user-attachments/assets/b63602c5-e7af-4724-9c0b-80413a919089)

We can remove the secret file .htpasswd from the node. Becasue secrets has been created and no point to store the file from the disk.

**To create a ConfigMap**

```
nano nginx.conf

//you can use below link to copy/paste the nginx.conf file

https://github.com/kohlidevops/DevOpsWithKubernetes/blob/main/12%20-%20Create%20ConfigMap%20and%20Secret%20From%20a%20File/nginx.conf

kubectl create configmap nginx-config-file --from-file nginx.conf
kubectl describe configmap nginx-config-file
```

**To create a pod**

```
nano nginx-pod.yaml

//you can use below link to copy/paste the nginx-pod.yaml file

https://github.com/kohlidevops/DevOpsWithKubernetes/blob/main/12%20-%20Create%20ConfigMap%20and%20Secret%20From%20a%20File/nginx-pod.yaml

kubectl apply -f nginx-pod.yaml
kubectl get pods -o wide
```

**To access the nginx with authentication**

```
curl <pods-ip>
//It will not access - Authorization faile
curl -u user:test123 <pods-ip>
//Now can access
```

