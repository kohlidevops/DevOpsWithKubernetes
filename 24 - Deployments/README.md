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

## Demo - Deployments in Kubernetes

SSH to master and execute the deployment manifest file

```
sudo -i
cd deployments
kubectl get nodes
kubect get pods -o wide
nano deployment.yaml

https://github.com/kohlidevops/DevOpsWithKubernetes/blob/main/24%20-%20Deployments/deployment.yaml

kubectl apply -f deployment.yaml
kubectl get deployments
kubectl get pods -o wide
kubectl get rs
```

![image](https://github.com/user-attachments/assets/395a968a-940c-496f-882f-8a7c020ff6ac)

_If you want to describe the deployment_

```
kubectl get deployments
kubectl describe deployment my-app
```

![image](https://github.com/user-attachments/assets/c77cb9a4-7e7d-4fda-a125-5b3584110e2f)

_To rollout the upgrade_

```
kubectl get deployment
kubectl set image deployment/<deployment-name> <container-name>=<Image-name>
kubectl set image deployment/my-app nginx-container=nginx:1.19
kubectl rollout status deployment <deployment-name>
kubectl rollout status deployment my-app
kubectl get pods --show-labels
```

![image](https://github.com/user-attachments/assets/d0f7244b-412a-4565-b01e-304c5180e2c4)

// It will upgrade the image one by one container instead of doing all at same time - Here application available at any time.

To check the rollout history

```
kubectl rollout history deployment my-app
```

![image](https://github.com/user-attachments/assets/48dbe2d6-3ba3-45d7-a66f-70bfffcddf6f)

Here record is missing! Thats is the problem. 

_Do the upgrade again with any other image version with record option_

```
kubectl set image deployment/my-app nginx-container=nginx:1.20 --record
kubectl rollout status deployment <deployment-name>
kubectl rollout status deployment my-app
kubectl rollout history deployment my-app
```

![image](https://github.com/user-attachments/assets/765dea99-6da5-4fe2-9ef9-bcdac7820e64)

Now history is available.

_If you describe the any one of the pod_

```
kubectl get pods --show-labels
kubectl describe pod <pod-name>
kubectl describe pod my-app-558b57bb8f-2f62j
```

![image](https://github.com/user-attachments/assets/b794394d-fb45-4877-8d5f-cbd70d36c856)

_To rollback your pod image_

```
kubectl rollout undo deployment <deployment-name>
kubectl rollout undo deployment my-app
kubectl rollout status deployment my-app
kubectl describe pod <pod-name>
kubectl describe pod my-app-8bd8b4c5c-2xh7w
```

![image](https://github.com/user-attachments/assets/f6c631fd-3fe2-4479-8f16-1f60e6bfb049)

_To rollout to specific revision_

```
kubectl rollout history deployment <deployment-name>
kubectl rollout history deployment my-app
kubectl rollout undo deployment my-app --to-revision=1
kubectl rollout status deployment my-app
kubectl rollout history deployment my-app
```

![image](https://github.com/user-attachments/assets/062a7ee3-d3de-4c7f-ad3c-3119731e8790)

_If you want to describe the pod_

```
kubectl  get pods --show-labels
kubectl describe pod <pod-name>
kubectl describe pod my-app-699d675655-5rc6c
```

![image](https://github.com/user-attachments/assets/8d5e0e88-74e4-44c2-b4d8-7194f72217df)


_To pause the deployment_

This will help when you are doing bulk changes in your deployment

```
kubectl rollout pause deployment <deployment-name>
kubectl rollout pause deployment my-app
kubectl set image deployment/my-app nginx-container=nginx:1.17 --record
kubectl rollout status deployment my-app
//Its "Waiting for deployment "my-app" rollout to finish: 0 out of 3 new replicas have been updated..."

kubectl get pods --show-labels
//Its still running old pod
```

![image](https://github.com/user-attachments/assets/99569c41-7fcc-4bc1-ac65-71b8a305033a)

_To resume the deployment_

```
kubectl rollout resume deployment <deployment-name>
kubectl rollout resume deployment my-app
kubectl rollout status deployment my-app
kubectl get pods --show-labels
```

Now it is resuming and doing all the things as we expected

![image](https://github.com/user-attachments/assets/68ad005b-3df5-49f0-8189-0402066abff1)

_To scaleup and scaledown your deployment_

```
kubectl scale deployment my-app --replicas=5
kubectl get pods --show-labels
kubectl scale deployment my-app --replicas=2
kubectl get pods --show-labels
```

![image](https://github.com/user-attachments/assets/92adb227-2dde-4520-9d8e-ad1a0ae293eb)



