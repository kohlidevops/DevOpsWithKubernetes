# Kubectl Management

**kubectl**

Kubectl is command line tool for Kubernetes.

Kubectl uses the K8s APIs internally to carryout the commands.

**kubectl get**

Kubectl get is used to get the objects, present in K8s Cluster

```
$ kubectl get <object_type> <object_name> -o <output> —sort-by <JSONpath> —selector <selector>

-o — Set Output format YML/JSON
-sort-by — Sort Output using JSON path Expression
-Selector — Filter results by label
```

**kubectl describe**

You can get Detailed Information about any Kubernetes Object.

```
kubectl describe <object_type> <object_name>
```

**kubectl create**

You can create any K8s Object using Kubectl create.

File descriptor must be YAML.

```
kubectl create -f <file_name>
```

**kubectl apply**

Kubectl apply is similar to Kubectl create.

If user use kubectl apply on already existing object. It will modify the existing object, if possible.

```
kubectl apply -f <file_name>
```

**kubectl create vs kubectl apply**

kubectl create - This command will create the resources defined in deployment.yaml. If the deployment already exists, the command will fail.

kubectl apply - This command will create the resources defined in deployment.yaml if they don’t exist, or update them if they already exist.

**kubectl delete**

Kubectl delete, deletes the object from K8s Cluster.

```
kubectl delete <object_type> <object_name>
```

**kubectl exec**

Kubectl exec, used to run commands inside container.

K8s resource must be running on which kubectl exec is being performed.

```
kubectl exec <pod_name> -c <conatiner_name>
```
