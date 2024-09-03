# How to Manage Container Resources in Kubernetes?

## Resource Request

It is something about that how many resource a particular container can claim.

➢ Resource request allows user to define a resource limit, that user expect a container to use.

➢ Kube Scheduler will manage resource request and avoid scheduling on node, which don’t have enough resources.

➢ Note : Containers are allowed to use more or less than the request resource. Resource Request is to manage the scheduling only.

➢ Memory is measure in Bytes. User is allowed to define in MegaByte as well.

➢ Requests for CPU resources are measured in cpu units. 1 vCPU means 1000 CPU Unit. If we mentioning 500m in cpu then that is half core of cpu

```
apiVersion: v1
kind: Pod
metadata: null
name: frontend
spec: null
containers:
  - name: app
image: nginx
resources: null
requests: null
memory: 64Mi
cpu: 250m
```

## Resource Limit

➢ Resource Limits used to Limit the container’s resource uses.

➢ Limits are imposed at RunTime Container.

```
apiVersion: v1
kind: Pod
metadata:
name: frontend
spec:
containers:
- name: app
image: nginx
resources:
limits:
memory: "128Mi"
cpu: "500m"
```

_What will happend if the container is reaching the cpu limits? The kubernetes will throttle the process and keep the container is running. But If the container is using that much of memory then Kubernetes will kill the container and restart the container as per your restart policy._

### Demo - Request Limit

SSH to K8 master node

```
sudo -i
kubectl get nodes
cd /root/pods_and_container
nano request_limit.yaml

https://github.com/kohlidevops/DevOpsWithKubernetes/blob/main/13%20-%20ManagingContainerResources/request_limit.yaml

kubectl apply -f request_limit.yaml
kubectl get pods -o wide
```

![image](https://github.com/user-attachments/assets/41dae5ca-8560-4b12-81a8-ee919cb15fa0)

Now i update the request_limit.yaml file with front-end 3 and 4 to change the cpu limit from 250 to 750m.

```
kubectl apply -f request_limit.yaml
```

I got error while running this pods - because its beyond the cpu limit.

![image](https://github.com/user-attachments/assets/1327fe3a-4764-4ffd-874a-73e7ce9ee915)

Now delete the pod and re-run it again and check the status.

```
kubectl delete -f request_limit.yaml
kubectl apply -f request_limit.yaml
```

![image](https://github.com/user-attachments/assets/b6a59e75-4adb-4f15-a295-863c847c1959)

The pod-4 is still pending. Because Kubernetes will not schedule this pods as it requires 750m cpu.

lets delete the request_limit pods

```
kubectl delete -f request_limit.yaml
```

### Resource Limit

```
cd /root/pods_and_container
nano resource_limit.yaml

https://github.com/kohlidevops/DevOpsWithKubernetes/blob/main/13%20-%20ManagingContainerResources/resource_limit.yaml

kubectl apply -f resource_limit.yaml
kubectl get pods -o wide
```

![image](https://github.com/user-attachments/assets/e012c91b-4aed-492a-932c-72bcc689040f)
