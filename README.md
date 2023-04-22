# HA-k8s with Ansible 

This repo contains a playbook to spin up a high-availability k8s cluster using stacked etcd (static pods). There are four main roles. The containerd and kubernetes roles gets all nodes ready with the aformentioned packages. The control_plane role sets-up the control plane nodes in a high-availablity configuration (one node is the main master, others are backups). Finally there is a playbook for the basic worker nodes. The main things you are reqired to do is to change the IP addresses of everything in the inventory and have a set of ubuntu 22.04 targets with SSH access. The assumption is made that there isn't already kubeadm initialized on any of these nodes, this would probably break things.

Common things you might want to change are:
 - k8s_api_address: the virtual ip address of the kubernetes api (192.168.1.9)
 - pod_cidr: cidr for the pods, this will be shared between calico and kubeadm init for you (172.18.0.0/16)
 - k8s_version: version of kubernetes (kubelet, kubeadm, kubectl) used across the nodes (1.27.0-00)

## Todo
 - Playbook to kubeadm reset everything in inventory
 - Playbook that spins up new workers if added to inventory (don't rebuild from scratch)
