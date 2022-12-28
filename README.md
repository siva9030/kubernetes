# kubernetes
#This repo for only k8s 

#This will guide you for installation steps.

#########################################################################
####################  Kubernetes Installation Steps  ##############################
#########################################################################

#On both master and Nodes
------------------------
#Be a root user. Install Docker and start Docker service. Also, enable the docker service so that the docker service starts on system restarts.

sudo su -
yum install docker -y 
systemctl enable docker && systemctl start docker

#Create proper yum repo files so that we can use yum commands to install the components of Kubernetes (just execute the below command, it will create kubernetes repo for you).

cat <<EOF > /etc/yum.repos.d/kubernetes.repo
[kubernetes]

name=Kubernetes

baseurl=https://packages.cloud.google.com/yum/repos/kubernetes-el7-x86_64

enabled=1

gpgcheck=1

repo_gpgcheck=0

gpgkey=https://packages.cloud.google.com/yum/doc/yum-key.gpg https://packages.cloud.google.com/yum/doc/rpm-package-key.gpg

exclude=kube*

EOF



#sysctl command is used to modify kernel parameters at runtime. Kubernetes needs to have access to kernel’s IP6 table and so we need to do some more modifications. This includes disabling secure Linux.

cat <<EOF >  /etc/sysctl.d/k8s.conf
net.bridge.bridge-nf-call-ip6tables = 1
net.bridge.bridge-nf-call-iptables = 1
EOF

sysctl --system
setenforce 0

#Install kubelet, kubeadm and kubectl; start kubelet daemon

yum install -y kubelet kubeadm kubectl --disableexcludes=kubernetes
systemctl enable kubelet && systemctl start kubelet


#Only on the Master Node:
========================
