# To upgrade the Kubernetes Cluster using kubeadm

First install the kubernetes cluster setup using below link

```
https://github.com/kohlidevops/DevOpsWithKubernetes/blob/main/2%20-%20Kubernetes%20Cluster%20Management/README.md
```

In this case, I have lauched 2 EC2 instance with k8 version - 1.29

![image](https://github.com/user-attachments/assets/86e61376-6911-4651-bfbe-d2172a00f609)

![image](https://github.com/user-attachments/assets/dd48972a-f453-4389-b37b-b69b99e49f99)


***************** Upgrade Control Plane Node ******************

**1. Get the Running Node and Version in k8 master node**

    kubectl get nodes


**2. Drain Master Node in k8 master node**

    kubectl drain <node-to-drain> --ignore-daemonsets

![image](https://github.com/user-attachments/assets/41cf5cde-eb4e-44d1-8a20-1ef05ee4958d)

**3. Update the Repository in k8 master node**

    sudo nano /etc/apt/sources.list.d/kubernetes.list
    //To change the version from 1.29 to 1.30
    [signed-by=/etc/apt/keyrings/kubernetes-apt-keyring.gpg] https://pkgs.k8s.io/core:/stable:/v1.30/deb/ /
    save it
     
**3. Upgrade kubeadm in k8 master node**

    sudo apt-get update
    sudo apt-get install -y --allow-change-held-packages kubeadm=1.30.0-1.1


**4. Verify that the download works and has the expected version in k8 master node**

    kubeadm version

![image](https://github.com/user-attachments/assets/5ab72169-3306-4941-8173-3d4b1b446912)


**5. Verify the upgrade plan in k8 master node**

    sudo kubeadm upgrade plan v1.30.0

![image](https://github.com/user-attachments/assets/cdd78f04-cabe-4799-a674-15e13f4b6d6c)


**6. Apply the Upgrade in k8 master node**

    sudo kubeadm upgrade apply v1.30.0

My cluster has been successfully upgraded

![image](https://github.com/user-attachments/assets/00747bfc-2f20-4074-b648-764990c63244)

**7. Upgrade kubelet and kubectl packages in k8 master node**

    sudo apt-get update
    sudo apt-get install -y --allow-change-held-packages kubelet=1.30.0-1.1 kubectl=1.30.0-1.1


**8. Restart the kubelet in k8 master node**

    sudo systemctl daemon-reload
    sudo systemctl restart kubelet


**10. Get the Running Node and Version in k8 master node**

    kubectl get nodes


**11. Uncordon the Node in k8 master node**

    kubectl uncordon <node-to-uncordon>

![image](https://github.com/user-attachments/assets/76b4fee8-0fee-45e3-af83-b2c215856beb)


  ****************** Upgrade Worker Node ********************


**1. Drain Worker Node in k8 master node**

    kubectl drain <node-to-drain> --ignore-daemonsets --force

![image](https://github.com/user-attachments/assets/d284b6f4-7ceb-4846-b811-33ccf6afdfe2)

**2. Upgrade kubeadm in worker node**

    sudo apt-get update
    sudo apt-get install -y --allow-change-held-packages kubeadm=1.30.0-1.1


**3. Verify that the download works and has the expected version in k8 worker node**

    kubeadm version


**4. For worker nodes this upgrades the local kubelet configuration in k8 worker node**

    sudo kubeadm upgrade node


**5. Upgrade kubelet and kubectl packages in worker node**

    sudo apt-get update
    sudo apt-get install -y --allow-change-held-packages kubelet=1.30.0-1.1 kubectl=1.30.0-1.1


**7. Restart the kubelet in worker node**

    sudo systemctl daemon-reload
    sudo systemctl restart kubelet


**8. Get the Running Node and Version in k8 master node**

    kubectl get nodes

![image](https://github.com/user-attachments/assets/be384446-d24c-445f-a172-e981ad922703)


**9. Uncordon the Node in k8 master node**

    kubectl uncordon <node-to-uncordon>

![image](https://github.com/user-attachments/assets/2e808874-6241-4619-8b81-75dc5c942763)

**9. To check the node version in k8 master**

   kubectl get nodes

![image](https://github.com/user-attachments/assets/4280a87c-aa6b-48c1-8a51-de121ca478b3)
