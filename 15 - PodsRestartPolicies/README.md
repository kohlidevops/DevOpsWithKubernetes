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
