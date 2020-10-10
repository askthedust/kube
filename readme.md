# Readme
Short description of the steps to reproduce the environment

## Requirements
- `Ansible` you can install using pip: `pip install -u ansible`
- `Virtualbox` as the hypervisor for `Vagrant`: [virtualbox](https://www.virtualbox.org/wiki/Downloads)
- `Vagrant` will be the wrapper to interact with `Virtualbox` to provide the VMs: [vagrant](https://www.vagrantup.com/downloads.html)  

## Configure the Vagrantfile
In the directory `vagrant` there is a file called `Vagrantfile` the current file version is configured to create 5 
VMs, composed as following: 
- 2 nodes (workers)
- 2 masters (controllers)
- 1 load balancer

Here also there are information about the IP addresses that will be configured. If you change them, you also have to 
change the in the file `playbooks/vars/generci_vars.yml` to be coherent with them. This is **important!**

### Steps to rollout and provisioning
1. In the *vagrant* directory rollout the VMs: `vagrant up`
2. Check the file *playbooks/vars/generic_vars.yml and if needed, just change the values to fit your environment
2. In the root of the project run ansible: `ansible-playbook playbooks/k8s.yml --diff -t hosts -K` 
   *If you didn't change IP addresses or any other information about about the hosts, you don't need to run thi command*
3. Still from the root of the project, run ansible: `ansible-playbook playbooks/k8s.yml --diff -K`