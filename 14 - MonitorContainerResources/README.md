# How to monitor Container Resources in Kubernets?

**Container Health**

➢ Kubernetes is feature Rich, and provide number of features to monitor the containers.

➢ Active Monitoring Helps K8s to decide the container state and Auto Restart in Case of Container Failure.

**Liveness Probe**

➢ Liveness probe helps to determine the Container State.

➢ By Default, K8s only consider container to be down, if container process stops.

➢ Liveness probe helps user to improve & customized this Container Monitoring mechanism.

➢ User can execute Two types of Liveness probes - Run Command in Container, Periodic HTTP Health Check. (If liveness healthcheck status is 200 then its fine, otherwise liveness is failed and kubernetes automatically restart the container.

➢ Liveness via Container Command manifest.

➢ initialDelaySeconds: How long to wait before sending a probe after a container starts.

➢ periodSeconds: How often a probe will be sent.

```
livenessProbe:
exec:
command:
-some command here-
initialDelaySeconds: 5
periodSeconds: 5
```

➢ Liveness via HTTP Request manifest.

➢ timeoutSeconds: How long a request can take to respond before it’s considered a failure.

```
livenessProbe:
httpGet:
path: /health.html
port: 8080
httpHeaders:
- name: Custom-Header
value: Awesome
initialDelaySeconds: 3
periodSeconds: 3
timeoutSeconds: 1
```

**Startup Probe**

➢ Setting up Liveness probe is very risky with Application which have Long StartUp Time.

➢ StartUp probe runs at container StartUp and stop running once container success.

➢ Once the startup probe has succeeded once, the liveness probe takes over to provide a fast response to container deadlocks.

_Suppose you have a complex application that needs a long time to initialize, like a database server that performs initial setup before it can accept connections. If you only had a liveness probe, Kubernetes might mistakenly restart the container before the application is fully ready. Here Startup probe came into the picture. The startup probe prevents the liveness probe from restarting the container before the application has fully started._

```
startupProbe:
httpGet:
path: /health.html
port: 8080
failureThreshold: 30
periodSeconds: 10
```

**httpGet:** This specifies that Kubernetes will perform an HTTP GET request to the /health.html path on port 8080 to determine if the application is ready.

**failureThreshold: 30:** This means that Kubernetes will allow up to 30 consecutive failures of the HTTP GET request before it decides that the startup has failed. In other words, if the /health.html endpoint does not respond successfully for 30 consecutive checks, Kubernetes will consider the container startup as failed.

**periodSeconds: 10:** This specifies how often Kubernetes will perform the probe. In this case, every 10 seconds, Kubernetes will send the HTTP GET request to /health.html.

Application will have a maximum of 5 minutes (30 * 10 = 300s) to finish its startup.

**Readiness Probe**

➢ Readiness is used to detect if a container is ready to accept traffic.

➢ Sometimes application might need to load large data or configuration files during startup, or depend on external services after startup.

➢ NO Traffic will be sent to a pod until container pass the Readiness Probe.

➢ Readiness and liveness probes can be used in parallel for the same container.

## Demo - Liveness Probe

SSH to K8 master node

```
sudo -i
cd pods_and_container
nano liveness-hc.yaml

https://github.com/kohlidevops/DevOpsWithKubernetes/blob/main/14%20-%20MonitorContainerResources/liveness-hc.yaml

kubectl get pods -o wide
kubectl describe pod liveness-probe

```

![image](https://github.com/user-attachments/assets/af8e6735-6cd5-437b-b578-c2b78cd802e1)

![image](https://github.com/user-attachments/assets/31084833-8fd2-429c-9df4-787f77820ac1)

**How It Works**

_Container Startup:_ When the container starts, it immediately creates the file /tmp/healthcheck, waits 60 seconds, then deletes the file, and finally sleeps for 10 minutes.

**_Liveness Probe Execution_:**

The livenessProbe checks the file /tmp/healthcheck using the cat command.

Since the file is deleted after 60 seconds, the cat /tmp/healthcheck command will fail after this time, causing the probe to fail.

**_Probe Timing:_**

_Initial Delay:_ 5 seconds before the first probe runs.

_Period:_ The probe will run every 5 seconds.

**_Given the container's behavior:_**

For the first 60 seconds, the file /tmp/healthcheck exists, so the cat command succeeds.

After 60 seconds, the file is deleted, and the cat command fails.

Since the probe runs every 5 seconds, it will fail after the file is deleted.

**_Expected Behavior:_**

The container will fail the liveness probe after 60 seconds because the file /tmp/healthcheck will no longer exist.

Kubernetes will detect the failed liveness probe and restart the container according to its restart policy.

Now the restart count is 6

![image](https://github.com/user-attachments/assets/4626e470-e57d-4e8c-8129-8946d4a25623)

## Demo - Liveness http probe

```
cd pods_and_container
nano liveness-hc-http-probe.yaml

https://github.com/kohlidevops/DevOpsWithKubernetes/blob/main/14%20-%20MonitorContainerResources/liveness-hc-http-probe.yaml

kubectl appy -f liveness-hc-http-probe.yaml
kubectl get pods -o wide
kubect describe pod liveness-probe-http
```

my container has been succesfully created. because this liveness probe checking path(/) with port 80.

## Demo - Startup Probe

```
cd pods_and_container
nano startup-hc.yaml

https://github.com/kohlidevops/DevOpsWithKubernetes/blob/main/14%20-%20MonitorContainerResources/startup-hc.yaml

kubectl apply -f startup-hc.yaml
kubectl get pods -o wide
```

**_How It Works_**

_Startup Probe Execution:_ Kubernetes performs an HTTP GET request to the / path on port 80 of the container to check if the container is ready to handle traffic.

_Initial Delay:_ There is no initialDelaySeconds specified, so the first probe starts immediately after the container is up.

_Period:_ The probe is performed every 10 seconds.

_Failure Threshold:_ If the HTTP request to / fails for 30 consecutive checks, Kubernetes will consider the container’s startup as failed. This threshold allows for a generous amount of time for the container to become ready.
        
![image](https://github.com/user-attachments/assets/6c839e42-9708-4349-a370-78e718972d03)

## Demo - Readiness Probe

```
sudo -i
cd pods_and_container
nano readiness-hc.yaml

https://github.com/kohlidevops/DevOpsWithKubernetes/blob/main/14%20-%20MonitorContainerResources/readiness-hc.yaml

kubectl apply -f readiness-hc.yaml
kubectl get pods -o wide
kubectl describe pod <pod-name>
kubectl describe pod hc-probe
```

![image](https://github.com/user-attachments/assets/384f9d2d-c96a-4679-99ec-6e967707271a)

Readiness probe is success that's why container has been running!

![image](https://github.com/user-attachments/assets/8207e2ce-23e2-40e6-9bf9-d2a14f575f5c)

Try to change the readiness port from 80 to 8080. My nginx applicaation is run with 80 port whereas now this readiness should probe the 8080. So it definetely failed.

For this first delete the hc-probe pod and change the probe port as below

![image](https://github.com/user-attachments/assets/5afaa81a-af80-4254-bc61-8923dec10e41)

```
kubectl delete pod hc-probe
after change the port
kubect apply -f readiness-hc.yaml
kubectl describe pod <pod-name>
kubectl describe pod hc-probe
```

![image](https://github.com/user-attachments/assets/6a704778-05e8-41bf-8151-337171cac41a)

my health probe is failed - As a result my container has not been up and running!


