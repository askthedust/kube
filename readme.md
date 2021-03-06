# Readme
This project is taking the original **Kelsey Hightower** [github](https://github.com/kelseyhightower/kubernetes-the-hard-way)
to who should be directed all the credits. There are small differences, to permit to run it in locally with VirtualBox,
and reusable with Ansible. My setup is a Mac and this is a pretty common. 
The goal is to have a working cluster locally, even with a balancer for the controllers, for testing purposes. 

## Requirements
- Python3, pip and virtualenv installed, for virtualenv use pip:
  - `pip install virtualenv`
- At least 8 GB of ram, there will be created 5 VMs (nodes 2GB each one, controllers and loadbalancer 1GB), in `Vagrantfile`
- `Virtualbox` as the hypervisor for `Vagrant`: [virtualbox](https://www.virtualbox.org/wiki/Downloads)
- `Vagrant` will be the wrapper to interact with `Virtualbox` to provide the VMs: [vagrant](https://www.vagrantup.com/downloads.html)
  
## Configure the Vagrantfile
In the directory `vagrant` there is a file called `Vagrantfile` which is configured to create 5 VMs, composed as following: 
- 2 nodes (workers)
- 2 masters (controllers)
- 1 load balancer

In the `Vagrantfile` there are also the information about IP addresses, memory an CPU for VMs. Changing IP addresses means 
you have to change them also here: `playbooks/inventory/group_vars/all.yml`. 

It is possible to change some values about the VMs, number of workers and controllers and ram:
```
configs:
    vbox_ubuntu_dist: "ubuntu/xenial64" 
    number_node: 2
    number_master: 2
    node_memory: 1024
    controller_memory: 1024
    loadbalancer_memory: 512
```

### Steps to rollout and provisioning
1. Create and run the python venv: `virtualenv -p python3 env && source env/bin/activate`
2. Install pip requirements: `pip install -r requirements.txt`
3. `cd vagrant` and run `vagrant up`, wait for the VMs are up and running
4. Back to the root of the project and run ansible to generate hostfile: `ansible-playbook playbooks/k8s.yml --diff -t hosts`
5. Run ansible again to provision the cluster: `ansible-playbook playbooks/k8s.yml --diff -K` 

- Pause the environment: `cd vagrant` and run `vagrant halt`
- Clean up: 
    - `cd vagrant` and run `vagrant destroy -f`
    - remove all the files in `k8s-certs`

### TODO
1. Improve the abstraction, currently many things are hardcoded
2. Add compatibility with newer version of ubuntu (or debian based)
3. Make the network plugin configurable
4. Add monitoring: prometheus and grafana
5. Add logs: grafana/loki
