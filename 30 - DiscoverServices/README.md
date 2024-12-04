# Discover Services in Kubernetes

➢ Kubernetes DNS assign DNSNames to Services, allow applications within Cluster to easily locate the Service.

➢ Service Fully Qualified Name has the following format- Service-name.namespace-name.svc.cluster-domain.example

➢ Default Cluster Domain is cluster.local

➢ Service fully qualified Domain Name can be used to reach service from within any Namespace in Cluster.

```
Service-name.namespace-name.svc.cluster.local
```

➢ Pods within the same NameSpace can use the Service Name Only - Service-name

## Lab - Discover Kubernetes Services

SSH to master node

```
sudo -i
kubectl get nodes
kubectl get services -o wide  (If I execute, then it will show nginx-service (ClusterIp as Service), nginx-service-nodeport (NodePort as Service) services as we created in last session)
```

![image](https://github.com/user-attachments/assets/9429883a-82bf-49ba-91f4-871c96108af1)

If I execute

```
kubectl get pods -o wide --show-labels
kubectl exec pod-svc-test -- curl nginx-service:8080
```

Then I can see all the pods. pod-svc-test pod also running which is created (dummy pod) to access the nginx-service.

![image](https://github.com/user-attachments/assets/31002656-dbbf-4a31-96a8-6d4244b0332f)

_To create a new namespace named service-namespace and create a pod in this name space and try to access the nginx-service using curl as before._

```
kubectl create namespace service-namespace
kubectl get ns
```

![image](https://github.com/user-attachments/assets/ecce2f18-3e6f-4f12-8792-b8d05b9730d7)

_To create a pod in the service-namespace
_
```
nano dns-service-pod.yaml

https://github.com/kohlidevops/DevOpsWithKubernetes/blob/main/30%20-%20DiscoverServices/dns-service-pod.yaml

kubectl apply -f dns-service-pod.yaml
kubectl get pods -o wide ( We cant able to see this pod. Becuase its created in different namespace - So we have to give namespace explicitly while get pods command)
kubectl get pods -o wide -n service-namespace
```

![image](https://github.com/user-attachments/assets/3396507c-bec9-41d9-80d2-7a23a4f5cf94)

_To access the nginx-service (default namespace) from dns-service pod (service-namespace) using curl_

```
kubectl exec -n <namespace-name> <pod-name> -- curl <service-name>:<port>
kubectl exec -n service-namespace svc-test-dns -- curl nginx-service:8080
```

![image](https://github.com/user-attachments/assets/7eecf64d-21bc-4bbd-8f8e-1a67c7e844b8)

We cant able to access the nginx-service from the dns-pod using curl with service-name (Becuase both are different namespace. So if we want to access the service from different namespace then we have to use fully qualified service name to access the service)

_To access the service with fully qualified service name_

```
kubectl exec -n <service-name> <pod-name> -- curl <service-name>.default.svc.cluster.local:<port>
kubectl exec -n service-namespace svc-test-dns -- curl nginx-service.default.svc.cluster.local:8080
```

![image](https://github.com/user-attachments/assets/933bb034-0c63-44cb-80d6-9e953c7d04d3)

**Same namespace - It should use service-name to access**

**Different namespace - It should use Fully Qualified Service Name to access**



