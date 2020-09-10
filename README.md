# k3s-cluster-ansible

This is an opinionated way to provision the OS and install k3s.

_Supported distros: **Debian 10.5** or **Ubuntu 20.04**_

## Prerequisites

There's a couple things that will need to be done before you get starting running with Ansible.

1) Install Ansible locally
2) Install a supported OS on each of your nodes
3) Set static IP for each node on the OS or in your router (you can use the IP assigned via DHCP, but it's not recommended)
4) Copy your local public ssh key with `ssh-copy-id` to each node
5) _Optional_ review playbooks and roles to understand what these Ansible script will do

After that we're ready to continue with Ansible...

## Ansible

Get started by cloning this repository and copying the hosts and config into a new directory.

```bash
# clone this repo
git clone https://github.com/k8s-at-home/k3s-cluster-ansible
# change into the directory
cd k3s-cluster-ansible
# copy the hosts and config to a new folder
cp -r ./inventory/local ./inventory/custom
```

### Update the Ansible config files

Update `./inventory/custom/hosts.yml` and `./inventory/custom/group_vars/all.yml` with the values that you want set. Each file it carefully documented.

### Run the playbooks

```
# This playbook will prepare your nodes for Kubernetes
ansible-playbook -i ./inventory/custom/hosts.yml ./playbooks/common.yml
# This playbook will install k3s
ansible-playbook -i ./inventory/custom/hosts.yml ./playbooks/cluster.yml
```

### Verify the cluster is up and running

```bash
kubectl --kubeconfig ./kubeconfig get nodes -o wide
```
