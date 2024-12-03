# Discover Services in Kubernetes

➢ Kubernetes DNS assign DNSNames to Services, allow applications within Cluster to easily locate the Service.

➢ Service Fully Qualified Name has the following format- Service-name.namespace-name.svc.cluster-domain.example

➢ Defauly Cluster Domain is cluster.local

➢ Service fully qualified Domain Name can be used to reach service from within any Namespace in Cluster.

```
Service-name.namespace-name.svc.cluster.local
```

➢ Pods within the same NameSpace can use the Service Name Only - Service-name
