# Deployments in Kubernetes

**Deployments**

➢ Deployment is one step higher than ReplicaSet.

➢ Deployment is desired State of ReplicaSet.

➢ Deployments control both ReplicaSets and Pods in a declarative manner.

➢ Smallest unit of Deployment, a Pod, runs containers. Each Pod has its own IP address and shares a PID namespace, network, and host name.

![image](https://github.com/user-attachments/assets/55c54784-4439-4237-b462-d516e2111f3b)

**Use Case of Deployment**

➢ Create Deployment : Deploy Application Pods.

➢ Update Deployment : Push new version of Application in Controlled Manner.

➢ Rolling Upgrade : Upgrade Application in Zero Downtime.

➢ Rollback : Rollback the Upgrade in case of unstable Upgrade. Revise the Deployment State.

➢ Pause/Resume Deployment : Rollout a certain percentage.

➢ Deployment RollOut Upgrade and Rollback Update.

![image](https://github.com/user-attachments/assets/71fceb08-8fce-45f5-9ee3-acaf57c27de0)

