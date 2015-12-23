# Rails Ansible
Ansible script for building Capistrano deploy-able Rails environment with Nginx, MySQL and Ubuntu Machine.

# How to Use

Assume we have Ubuntu servers with an user having no-password sudo rights.



# Quick Excercise

We can try out this script on virtual environment.
Assume, we have vagrant installed, and have enough memory to allocate them.

1. Spin up a VM with Vagrant
```
$ vagrant up # Configured in Vagrantfile
```

2. Install Ansible to local machine
```
$ pip install -r requirements.txt
// Or Simply,
$ pip install ansible
```

3. Upload SSH public key to the vagrant machine
```
$ cat ~/.ssh/id_rsa.pub (host machine)
# Copy the output
$ vim ~/.ssh/authorized_keys (guest machine)
```

4. Run ansible playbook
```
$ ansible-playbook -i hosts vagrant.yml -u vagrant
```

We get the server configured correctly unless hitting errors.

