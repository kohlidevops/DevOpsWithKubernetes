# Install Minikube on ubuntu-22

Launch Ubuntu-22 based EC2 instance with t3.medium and SSH to instance 

Install Kubernetes using MiniKube

********** Install Docker CE Edition **********

**1. Uninstall old versions**

    sudo apt-get remove docker docker-engine docker.io containerd runc


**2. Update the apt package index**

    sudo apt-get update

    sudo apt-get install apt-transport-https ca-certificates curl gnupg lsb-release


**3. Add Docker’s official GPG key:**

    curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg

**4. Use the following command to set up the stable repository**

    echo \  "deb [arch=amd64 signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu \  $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

**5. Install Docker Engine**

    sudo apt-get updatesudo apt-get install docker-ce docker-ce-cli containerd.io
**
6. verify Docker version**

    docker --version

********** Install KubeCtl **********

**1. Download the latest release**

    curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"


**2. Install kubectl**

    sudo install -o root -g root -m 0755 kubectl /usr/local/bin/kubectl

**3. Test to ensure the version you installed is up-to-date:**

    kubectl version --client


********** Install MiniKube **********

**1. Download Binay**

    curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64chmod +x minikube-linux-amd64

**2. Install Minikube**

    sudo install minikube-linux-amd64 /usr/local/bin/minikube


**3. Verify Installation**

    minikube version


**4. Start Kubernetes Cluster**

    sudo apt install conntracksudo minikube start --vm-driver=none


**5. Get Cluster Information**

    kubectl config view
