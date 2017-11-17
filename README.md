Original: http://jeremievallee.com/2017/01/31/kubernetes-with-vagrant-ansible-kubeadm/

# kubernetes-vagrant-ansible
Install Kubernetes on Vagrant (libvirt) using Ansible.

## Requirements

- Vagrant (with libvirt and proxyconf plugins)
- libvirt and dependencies
- Ansible

## Steps

### Create virtualenv for ansible
```
virtualenv ~/venv/multikube
. ~/venv/multikube/bin/activate
pip install ansible
```

### Install Vagrant and plugins

sudo apt install <libvirt bits>

install latest vagrant from https://www.vagrantup.com/downloads.html (2.0.1)
install vagrant-libvirt plugin

sudo apt install libxslt-dev libxml2-dev libvirt-dev zlib1g-dev ruby-dev
# https://github.com/vagrant-libvirt/vagrant-libvirt
vagrant plugin install vagrant-libvirt

# https://github.com/tmatilai/vagrant-proxyconf
vagrant plugin install vagrant-proxyconf


First, create the machines.

```
vagrant up --provider=libvirt
```

Then, provision the machines.

```
sudo apt install sshpass

ANSIBLE_HOST_KEY_CHECKING=False ansible-playbook -vv playbook.yml -i inventory -e @vars.yml

```


