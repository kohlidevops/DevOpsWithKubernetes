# Create a Kubernetes Cluster setup with High Availability using kubeadm

### Launch EC2 instances

To launch 3 EC2 instances with ubuntu-22 as 1 Control plane and 2 Data plane nodes.

![image](https://github.com/user-attachments/assets/780ac39d-c99f-49e6-9d19-6283e78910a2)

## Install on Master Node and worker nodes

### Step-1: Enable iptables Bridged Traffic on all the Nodes

```
sudo -i
cat <<EOF | sudo tee /etc/modules-load.d/k8s.conf
overlay
br_netfilter
EOF

sudo modprobe overlay
sudo modprobe br_netfilter

# sysctl params required by setup, params persist across reboots
cat <<EOF | sudo tee /etc/sysctl.d/k8s.conf
net.bridge.bridge-nf-call-iptables  = 1
net.bridge.bridge-nf-call-ip6tables = 1
net.ipv4.ip_forward                 = 1
EOF

# Apply sysctl params without reboot
sudo sysctl --system
```

### Step-2: Disable swap on all the Nodes

```
sudo swapoff -a
(crontab -l 2>/dev/null; echo "@reboot /sbin/swapoff -a") | crontab - || true
```

### Step-3: Install CRI-O Runtime On All The Nodes

```
sudo apt-get update -y
sudo apt-get install -y software-properties-common curl apt-transport-https ca-certificates

curl -fsSL https://pkgs.k8s.io/addons:/cri-o:/prerelease:/main/deb/Release.key |
    gpg --dearmor -o /etc/apt/keyrings/cri-o-apt-keyring.gpg
echo "deb [signed-by=/etc/apt/keyrings/cri-o-apt-keyring.gpg] https://pkgs.k8s.io/addons:/cri-o:/prerelease:/main/deb/ /" |
    tee /etc/apt/sources.list.d/cri-o.list

sudo apt-get update -y
sudo apt-get install -y cri-o

sudo systemctl daemon-reload
sudo systemctl enable crio --now
sudo systemctl start crio.service
```

### Step-4: To install crictl

```
VERSION="v1.28.0"
wget https://github.com/kubernetes-sigs/cri-tools/releases/download/$VERSION/crictl-$VERSION-linux-amd64.tar.gz
sudo tar zxvf crictl-$VERSION-linux-amd64.tar.gz -C /usr/local/bin
rm -f crictl-$VERSION-linux-amd64.tar.gz
```

### Step-5: Install Kubeadm & Kubelet & Kubectl on all Nodes

```
KUBERNETES_VERSION=1.29

sudo mkdir -p /etc/apt/keyrings
curl -fsSL https://pkgs.k8s.io/core:/stable:/v$KUBERNETES_VERSION/deb/Release.key | sudo gpg --dearmor -o /etc/apt/keyrings/kubernetes-apt-keyring.gpg
echo "deb [signed-by=/etc/apt/keyrings/kubernetes-apt-keyring.gpg] https://pkgs.k8s.io/core:/stable:/v$KUBERNETES_VERSION/deb/ /" | sudo tee /etc/apt/sources.list.d/kubernetes.list

sudo apt-get update -y

sudo apt-get install -y kubelet kubeadm kubectl
sudo apt-mark hold kubelet kubeadm kubectl
```

## Install on Master node only

### Step-6: Initialize Kubeadm On Master Node To Setup Control Plane

I'm go with Master node with Private IP Address

```
IPADDR="10.0.0.10"  //Replace your Master EC2 instance Private IP address
NODENAME=$(hostname -s)
POD_CIDR="192.168.0.0/16"
```

Kubeadm init command to initialize the setup

```
sudo kubeadm init --apiserver-advertise-address=$IPADDR  --apiserver-cert-extra-sans=$IPADDR  --pod-network-cidr=$POD_CIDR --node-name $NODENAME --ignore-preflight-errors Swap
```

##### If you are facing issues like below

        error execution phase preflight: [preflight] Some fatal errors occurred:
        [ERROR FileContent--proc-sys-net-bridge-bridge-nf-call-iptables]: /proc/sys/net/bridge/bridge-nf-call-iptables does not exist


#### Then execute below command to resolve then continue

        modprobe br_netfilter
        echo 1 > /proc/sys/net/bridge/bridge-nf-call-iptables
        echo 1 > /proc/sys/net/ipv4/ip_forward

To use the following commands from the output to create the kubeconfig in master so that you can use kubectl to interact with cluster API.

```
mkdir -p $HOME/.kube
sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
sudo chown $(id -u):$(id -g) $HOME/.kube/config
```

Now, verify the kubeconfig by executing the following kubectl command to list all the pods in the kube-system namespace.

```
kubectl get po -n kube-system
```

You can fire this command to get token and use this token when you join the worker nodes to the master node

```
kubeadm token create --print-join-command
```

## Install on all the Worker nodes

### Step-7: Join Worker Nodes To Kubernetes Master Nodes

SSH to all the worker nodes

```
sudo -i
sudo kubeadm join 10.128.0.37:6443 --token aaaaaaaaaaaaaaaaaaaaaaa \
    --discovery-token-ca-cert-hash sha256:1111111112222222222aaaaaaaaaaaaabbbbbbbbbbbccccccccc
```

### Logon to the master node and check the status

```
kubectl get nodes
```

![image](https://github.com/user-attachments/assets/0122cd17-ee43-4d5d-b234-e34486487f06)

## Install Calico networking on the Master node

### Step-8: Install Calico Network Plugin for Pod Networking

```
kubectl apply -f https://docs.projectcalico.org/manifests/calico.yaml
kubectl get po -n kube-system
```





