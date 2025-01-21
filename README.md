# Kubernetes on Mac using Vagrant UTM

Vagrant setup for a 3 node Kubernetes cluster on Mac using UTM.

> Adheres to official documentation : [Creating a cluster with kubeadm](https://kubernetes.io/docs/setup/production-environment/tools/kubeadm/create-cluster-kubeadm/)

## Prerequisites
* [Vagrant](https://www.vagrantup.com/)
* [UTM](https://mac.getutm.app/)
* [Vagrant UTM plugin](https://naveenrajm7.github.io/vagrant_utm/)
* [Ansible ](https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html)

## How to use

1. Clone repo
```bash
git clone https://github.com/naveenrajm7/K8s-utm.git
```

2. Execute vagrant inside folder
```bash
cd K8s-utm
vagrant up
```

3. Access master and use Kubernetes
```bash
# Accessing master
$ vagrant ssh k8s-master
...
vagrant@k8s-master:~$ kubectl get nodes
NAME         STATUS   ROLES           AGE     VERSION
k8s-master   Ready    control-plane   8m33s   v1.32.1
node-1       Ready    <none>          5m56s   v1.32.1
node-2       Ready    <none>          3m3s    v1.32.1
```

## Credits

Based of [naveenrajm7/k8s-setup](https://github.com/naveenrajm7/k8s-setup), updated to work with Vagrant UTM and Kubernetes 1.32 on Debian 12.
