# Dev-Ops

## Overview
This is the Real Technology Solutions Dev-Ops for it's servers.

## Requirements
Multiple servers (control plane + workers) all assumed to be RHEL based. Tested with Centos Stream 9.

## Installation
To run a fresh installation:

1. Update/Create a hosts file to fit the currently setup of the systems in it's own inventory directory.

2. SSH to your servers to ensure you have the fingerprints accepted as known.

2. Run the following command to initialize a user and ssh for auth.

``` shell
ansible-playbook -kK -i inventories/<Your inventory name> init.yaml
```

3. Run the following command to install roles

``` shell
ansible-playbook -i inventories/<Your inventory name> main.yaml
```

## Reset

If you want to reset kubeadm, effectively restarting the k8s cluster from scratch with no nodes connected or control panels setup run:

``` shell
ansible-playbook -i inventories/<Your inventory name> reset.yaml
```

## Join
If you have reset your kubeadm and want to setup control nodes and rejoin workers without going through the install process run:

``` shell
ansible-playbook -i inventories/<Your inventory name> join.yaml
```


## todo Update



## Todo List:

- CA Janitor
- Vault
- ArgoCD
- Github Action Workers
- Artifactory?
- simplify roles (1 yum role, no crds in settings, etc)



ansible-playbook -kK -i inventories/rts-k8s ./plays/init.yaml
ansible-playbook -i inventories/rts-k8s ./plays/devops-stack-install.yaml
ansible-playbook -i inventories/rts-k8s ./plays/debug.yaml
ansible-playbook -i inventories/rts-k8s ./plays/reset-kubedm.yaml
ansible-playbook -i inventories/rts-k8s ./plays/fetch-k8sconfig.yaml

get expiry: openssl x509 -enddate -noout -in ca.crt
check if will expire within week: openssl x509 -checkend 604800 -noout -in ca.crt

kubeadm join 192.168.56.104:6443 --token lhxxbh.efq6sb6zmh62ckjc --discovery-token-ca-cert-hash sha256:41a8aa76d4c53c78f8fea1c815fc97e26873f729080783205b183f6acf3cd1ae --control-plane --certificate-key c881fc1701030ccb26b0ce08005f3a773c109b705c5213caf7c65cccfaff2ca9 --apiserver-advertise-address=192.168.56.103

kubeadm init --apiserver-advertise-address={{ ansible_ssh_host }} --control-plane-endpoint={{ ansible_ssh_host }}

kubeadm init phase upload-certs --upload-certs --config=/etc/kubernetes/admin.conf

echo $(kubeadm token create --print-join-command) --control-plane --certificate-key $(kubeadm init --apiserver-advertise-address=192.168.56.104 --control-plane-endpoint=192.168.56.104 phase upload-certs --upload-certs --config /home/rts-k8s/.kube/config | grep -vw -e certificate -e Namespace)
