# Pods Restart Policies in Kubernetes

**Restart Policies**

➢ Kubernetes have capability to Auto Restart the containers when they fails.

➢ RestartPolicies customize the K8s Container Restart behaviour and you can choose when to Restart the Containers.

➢ K8s have three restartPolicies - Always, OnFailure & Never

**_Always Restart Policy_**

➢ Always is default restart policy in K8s.

➢ With Always Policy, containers always restart even if container completed successfully.

➢ This policy is recommended for containers that should always be in running state. 

**_OnFailure Restart Policy_**

➢ OnFailure is only works, if container Process exit with Error code.

➢ It also works if container liveness probe determine the container unhealthy.

➢ Use this policy on application that needs to be run successfully and then Stop.

**_Never Restart Policy_**

➢ Never allow container to never restart even the container liveness probe failed.

➢ Use this for application that Run only Once and never automatically restarted.

![image](https://github.com/user-attachments/assets/5bd83143-94ff-45bf-b09a-2e8468b4e672)


## Demo - Always Restart Policy

```
sudo -i
cd pods_and_container
nano always-restart.yaml

https://github.com/kohlidevops/DevOpsWithKubernetes/blob/main/15%20-%20PodsRestartPolicies/always-restart.yaml

kubectl apply -f always-restart.yaml
kubectl get pods -o wide
```

Restarting the container continuously

![image](https://github.com/user-attachments/assets/d9db4a67-833d-4347-baaa-9ad626553a43)

## Demo - Onfailure Restart Policy

```
cd pods_and_container
nano onfailure-restart.yaml

https://github.com/kohlidevops/DevOpsWithKubernetes/blob/main/15%20-%20PodsRestartPolicies/onfailure-restart.yaml

kubectl apply -f onfailure-restart.yaml
kubectl get pods -o wide
```

Now my pod is not restarting! Why? - Because my container has been exited successfully after sleep with 20 seconds. 

![image](https://github.com/user-attachments/assets/77a4c074-8ec8-4cdb-828e-04039ce62689)

Container will restart when failure occurs.

## Demo - onfailure Restart Policy with (Reprodcing restart)

```
cd pods_and_container
nano onfailure-restart-reproduce.yaml

https://github.com/kohlidevops/DevOpsWithKubernetes/blob/main/15%20-%20PodsRestartPolicies/onfailure-restart-reproduce.yaml

kubectl apply -f onfailure-restart-reproduce.yaml
kubect get pods -o wide
```

## Demo - Never Restart Policy

```
cd pods_and_container
nano never-restart.yaml

https://github.com/kohlidevops/DevOpsWithKubernetes/blob/main/15%20-%20PodsRestartPolicies/never-restart.yaml

kubectl apply -f never-restart.yaml
kubectl get pods
```

Container has been exited successfully after sleep 20 seconds - But it never restarts!

![image](https://github.com/user-attachments/assets/4b4c6fec-70f6-43eb-9b03-eb81073ae11b)

