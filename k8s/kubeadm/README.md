
# Creating a cluster with kubeadm 
Reference: https://kubernetes.io/docs/setup/production-environment/tools/kubeadm/create-cluster-kubeadm/  

## Requirements  
2 CPUs
2 GB RAM per machine

# Install Pre-requisites

## Component installation
Install the container runtime

## Install containerd
https://docs.docker.com/engine/install/ubuntu/  

```
# Add Docker's official GPG key:
sudo apt-get update
sudo apt-get install ca-certificates curl
sudo install -m 0755 -d /etc/apt/keyrings
sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc
sudo chmod a+r /etc/apt/keyrings/docker.asc

# Add the repository to Apt sources:
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/ubuntu \
  $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt-get update
```
Install Docker packages
```
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```

Verify that the Docker Engine installation is successful by running the hello-world image.
```
sudo docker run hello-world
```

### Install CNI containerd plugins
https://github.com/containerd/containerd/blob/main/docs/getting-started.md#step-3-installing-cni-plugins  

### Configure the `systemd` cgroup driver
https://kubernetes.io/docs/setup/production-environment/container-runtimes/#containerd-systemd  

### Install crictl
https://kubernetes.io/docs/tasks/debug/debug-cluster/crictl/#installing-crictl  

## Network setup
[Source](https://phoenixnap.com/kb/install-kubernetes-on-ubuntu)

Open the **kubernetes.conf** to configure Kubernetes networking
sudo nano /etc/sysctl.d/kubernetes.conf

```
Add the following lines
net.bridge.bridge-nf-call-ip6tables = 1
net.bridge.bridge-nf-call-iptables = 1
net.ipv4.ip_forward = 1
```

Reload the configuration by typing:
```
sudo sysctl --system
```

#### Assign Hostname for each Server Node

sudo hostnamectl set-hostname master-node  



## Install kubeadm 
[Kubernetes doc](https://kubernetes.io/pt-br/docs/setup/production-environment/tools/kubeadm/install-kubeadm/#instalando-o-kubeadm-kubelet-e-o-kubectl)

### Install kubeadm, kubelet, kubectl
```
sudo snap install kubeadm --classic
sudo snap install kubelet --classic
sudo snap install kubectl --classic
```

Tutorial used  
https://phoenixnap.com/kb/install-kubernetes-on-ubuntu  

Right repos
https://kubernetes.io/blog/2023/08/15/pkgs-k8s-io-introduction/  

That repo above will install version 1.28.8

```
sudo apt install kubeadm kubelet kubectl -y
```


### Pull kubeadm base images
```
kubeadm config images pull
```

### Initialize kube adm
```
kubeadm init
```

## Join Nodes

```
mkdir -p $HOME/.kube
sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
sudo chown $(id -u):$(id -g) $HOME/.kube/config 
```

```
kubeadm join ...
```