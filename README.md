# Ansible Rails ![License](http://img.shields.io/:license-mit-blue.svg?style=flat-square)

Ansible script for building Capistrano deploy-able Rails environment with Nginx and MySQL on Ubuntu Machine.

This project aims to (1) automate to build Rails environment and (2) provide the Rails configuration examples to releave the pain of setting these stuff by hand.

|| Remarks |
|---|---|
|Ubuntu| >= 14.04 |
|Ruby on Rails| |
|Unicorn| |
|MySQL| |
|Nginx| Currently SSL certificate is not setted |
|Rbenv| |


# How to Use

Assume we have Ubuntu servers with an user having no-password sudo rights.
If the user does not have this rights, please execute a following command (edit `username`).
```
echo "username ALL=(ALL) NOPASSWD:ALL" >> /etc/sudoers
```

- Edit configuration of ansible
  - `ansible/group_vars/rails`
  - `ansible/hosts` # Specify the IP address

- Install Ansible
```
$ pip install -r requirements.txt
```

- Execute Ansible (edit `username`)
```
$ ansible-playbook -i hosts rails.yml -u username
```

- Edit your rails environment (We have sample configuration under `rails_config`)
- Execute Capsitrano (e.g. `cap staging deploy`)

# TODO

Following features will be supported in the future release.
Your pull requests related/not-related these features are really appreciated.

- Automate SSL configuration for Nginx
- Automate Password-less sudo user setting

# Quick Excercise with Vagrant

Assume, we have vagrant installed, and have enough memory to allocate them.

- Spin up a VM with Vagrant
```
$ vagrant up # the same hierarchy with Vagrantfile
```

- Install Ansible to local machine
```
$ pip install -r requirements.txt
```

- Upload SSH public key to the vagrant machine
```
$ cat ~/.ssh/id_rsa.pub (host machine)
# Copy the output
$ vim ~/.ssh/authorized_keys (guest machine)
# Paset the SSL public key
```

- Run ansible playbook
```
$ ansible-playbook -i hosts vagrant.yml -u vagrant
```

Now, we get the server prepared for Rails deployment unless hitting some errors.

`Assume you have some rails project hosted in Github`

- Upload your Vagrant's SSH public key to Github as a deploy key

- Configure Unicorn and Capistrano configuration according to `rails_config` examples

- Execute Capistrano
```
$ cap staging deploy
```

Then, we can access your Rails service via `http://192.168.33.3`
