
# Application Configuration in Kubernetes

**What is Application Configuration?**

Kubernetes allows user to pass dynamic configuration values to application at Runtime.

These dynamic Configuration helps user to control the Application Flow.

**ConfigMap**

➢ Keep the Non-Sensitive Data in ConfigMap, which can be passed to Container Application.

➢ Config Map Store Data in Key-Value format.

➢ ConfigMaps allow you to separate your configurations from your Pods and components.

➢ ConfigMap helps to makes configurations easier to change and manage, and prevents hardcoding configuration data to Pod specifications.

**ConfigMap Commands**

Config Map via Config File.

```
kubectl create configmap [NAME] --from-file [/PATH/TO/ FILE.PROPERTIES] --from-file [/PATH/TO/FILE2.PROPERTIES]
kubectl create configmap [NAME] --from-file [/PATH/TO/ DIRECTORY]
```

Get ConfigMap via CLI.

```
kubectl get configmap <Config_map_name> -o yaml/json
```

**Secrets**

➢ Secrets are similar to ConfigMap but designed to keep the Sensitive Data.

➢ Create Secrets from file.

```
kubectl create secret generic db-user-pass --from-file=./username.txt —from-file=./password.txt
```

➢ Note : Special characters such as $, \, *, and ! require escaping.

➢ Get Secrets.

```
kubectl get secrets
```

➢ Describe Secrets.

```
kubectl describe secrets <Secret_name>
```

![image](https://github.com/user-attachments/assets/b084f12c-715e-4d04-bb37-d238bcea6eff)


![image](https://github.com/user-attachments/assets/9bb13667-7ef8-4cf9-bf18-7c44e18a88f6)

![image](https://github.com/user-attachments/assets/63c712c7-5141-499b-9c43-548f4c43a2c1)

