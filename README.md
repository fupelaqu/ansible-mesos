# Ansible Playbook for Mesos

This is an [Ansible](http://www.ansibleworks.com/) playbook for [Mesos](http://mesosphere.io/). You can use it by itself or as part of a larger playbook customized for your local environment.

## Testing locally with Vagrant
A sample [Vagrant](http://www.vagrantup.com/) configuration is provided to help with local testing. After installing Vagrant, run `vagrant up` at the root of the project to get a VM instance bootstrapped and configured with a running instance of Mesos.

## Include role in a larger playbook
### Add this role as a git submodule
Assuming your playbook structure is such as:
```
- my-master-playbook
  |- vars
  |- roles
  |- my-master-playbook-main.yml
  \- my-master-inventory.ini
```

Checkout this project as a submodule under roles:

```
$  cd roles
$  git submodule add git://github.com/fupelaqu/ansible-mesos.git ./ansible-mesos
$  git submodule update --init
$  git commit ./ansible-mesos -m "Added submodule as ./ansible-mesos"
```

### Include this playbook as a role in your master playbook
Example `my-master-playbook-main.yml`:

```
---

#########################
# Mesos install #
#########################

- hosts: all_mesos
  user: ubuntu
  sudo: yes

  roles:
    - ansible-mesos

  vars_files:
    - vars/my-vars.yml
```

# Issues, requests, contributions
This software is provided as is. Having said that, if you see an issue, feel free to log a ticket. We'll do our best to address it. Same if you want to see a certain feature supported in the fututre. No guarantees are made that any requested feature will be implemented. If you'd like to contribute, feel free to clone and submit a pull request.

# Dependencies
None

# License
MIT

# Author Information

Stéphane Manciot - stephane.manciot [at] gmail.com
