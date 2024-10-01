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





