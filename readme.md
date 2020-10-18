# Readme
This project is taking the original **Kelsey Hightower** [github](https://github.com/kelseyhightower/kubernetes-the-hard-way)
which should be directed all the credits, with some small modification, to permit to run it in local with VirtualBox,
and reusable with Ansible. My setup is a Mac and this is a pretty common. 
The goal is to have a working cluster locally, even with a balancer for the controllers, for testing purposes. 

## Requirements
- `Python3` already installed
- At least 10 GB of ram, there will be created 5 VMs with 2GB of ram each one, you can change to 1GB in `Vagrantfile`
- `Virtualbox` as the hypervisor for `Vagrant`: [virtualbox](https://www.virtualbox.org/wiki/Downloads)
- `Vagrant` will be the wrapper to interact with `Virtualbox` to provide the VMs: [vagrant](https://www.vagrantup.com/downloads.html)
  
## Configure the Vagrantfile
In the directory `vagrant` there is a file called `Vagrantfile` which is configured to create 5 VMs, composed as following: 
- 2 nodes (workers)
- 2 masters (controllers)
- 1 load balancer

In the `Vagrantfile` there are also the information about IP addresses, memory an CPU for VMs. Changing IP addresses means 
you have to change them also here: `playbooks/vars/generci_vars.yml`. 

### Steps to rollout and provisioning
1. Create and run the python venv: `python3 -m venv env && source env/bin/activate`
2. Install pip requirements: `pip install -r requirements.txt`
3. `cd vagrant` and run `vagrant up`, wait for the VMs are up and running
4. Back to the root of the project and run ansible: `ansible-playbook playbooks/k8s.yml --diff -K` 
