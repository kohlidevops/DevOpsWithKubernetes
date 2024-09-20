# Services in Kubernetes

➤ Service is used to Access the Application Running on Pods.

➤ Pods are Dynamic in Kubernetes, Pods created and terminated on Demand.

➤ Using Replication Controller, Pods are created and Terminated during the Scaling.

➤ Using Deployments, Pods are Terminated and new Pods are take place during the Image Version Upgrade.

➤ Pod’s can’t be accessed directly, but thru a Service.

➤ Kubectl Expose command created a Service for Pods so that they can be accessible Externally.

➤ Creating a Service will create and End-Point for Pods.

➤ The set of Pods targeted by a Service is usually determined by a selector in manifest file.

➤ Publish Service, Service Type.

➤ ClusterIP: Exposes the Service on a cluster-internal IP. Choosing this value makes the Service only reachable from within the cluster.

➤ NodePort: Exposes the Service on each Node’s IP at a static port. You’ll be able to contact the NodePort Service, from outside the cluster, by requesting <NodeID>:<NodePort>

➤ Load Balancer: Exposes the Service externally using a cloud provider’s load balancer. NodePort and ClusterIP Services, to which the external load balancer routes, are automatically created.

➤ External Name : Maps the Service to the contents of the external name field, by returning a CNAME record.
