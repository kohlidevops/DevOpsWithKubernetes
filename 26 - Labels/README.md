# Labels in Kubernetes

➤ Labels are key/value pairs that are attached to objects.

➤ Labels are intended to be used to specify identifying attributes of objects that are meaningful and relevant to users.

➤ Labels are like Tags in Cloud Providers like AWS , GCP.

➤ Labels can be attached to objects at creation time and subsequently added and modified at any time.

➤ For Labels you can follow Key-Value Pair Structure like.

```
Key: environment - Value: dev/qa/UAT/prod
Key: department - Value: engineering/cloudops/QA
```

➤ configuration file for a Pod that has two labels

environment: production and app: nginx

![image](https://github.com/user-attachments/assets/40d71aca-86cf-4452-b31b-fb71099f46ab)

➤ Labels are not Unique and multiple Labels can be added to One Object.

➤ Once Labels are attached to object, we can filter the results on Labels.

➤ Above approach is Called Label-Selector.

➤ Using Label Selectors user can use matching expressions to match Labels.

➤ Sample Matching:

```
environment = production
tier != backend
environment in (production, qa, UAT)
tier notin (frontend, backend)
```

➤ User can use Labels to tag Nodes

➤ Once Nodes are tagged, user can use label Selectors to run Pods only on matching Nodes.

➤ Tag Node Like:

```
kubectl get nodes
kubectl label nodes <your-node-name> disktype=ssd
kubectl get nodes --show-labels
```

➤ Run Pods on Specific Nodes by nodeSelector.

![image](https://github.com/user-attachments/assets/30a8ce2a-897b-43c7-9238-32cec2108998)

## Lab: Labels in Kubernetes

To start master and 2 worker nodes for this lab and SSH to master node

```
sudo -i
kubectl get nodes
kubectl get nodes --show-labels
```

![image](https://github.com/user-attachments/assets/254ff49e-155f-4140-a763-951359551d7b)

//To check if any node has label called "disktype=ssd"

//yes one node has it

_To run the label-pod yaml file and check_

//In my yaml file, I have mentioned nodeSelector - disktype: ssd

```
nano label-pod.yaml

https://github.com/kohlidevops/DevOpsWithKubernetes/blob/main/26%20-%20Labels/label-pod.yaml

kubectl apply -f label-pod.yaml
kubectl get pods -o wide
kubectl describe pod <pod-name>
kubectl describe pod nginx-web
```

![image](https://github.com/user-attachments/assets/cea26139-942e-4232-a6e7-2339a0d0f59f)

Yes it has been assigned to the particular worker node. If you describe then,

![image](https://github.com/user-attachments/assets/19a3a0e5-b558-438a-ad4c-57069981ac64)

_To remove the label and check again_

```
kubectl get nodes --show-labels
kubectl label node <node-name> <label>-  //- should be add at the end of line
kubectl label node ip-172-31-47-215 disktype-
kubectl get nodes --show-labels
kubectl delete pod <pod-name>
kubectl delete pod nginx-web
```

_To run again the label-pod yaml file_

```
kubectl apply -f label-pod.yaml
kubectl get pods -o wide
kubectl describe pod nginx-web
```

![image](https://github.com/user-attachments/assets/65eb3e52-4735-437f-af08-4cabd27ba41e)

Still its pending! If you describe it

![image](https://github.com/user-attachments/assets/1efbc78e-bf48-46b4-afd5-84ded6689a77)

_To add the label again_

```
kubectl label node ip-172-31-47-215 disktype=ssd
kubectl get nodes --show-labels
```

![image](https://github.com/user-attachments/assets/de2c5a3d-8282-4f45-ba92-571d01beae2c)

Now the pod has been assigned to the worker node - Because label has been assigned

![image](https://github.com/user-attachments/assets/3e0e14f2-b81d-4144-be2b-91a1e0f42dfd)








