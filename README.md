# Ansible Rails Enterprise Provisioner

### Environment Assumptions:

##### Control Machine:

* [Ansible](http://www.ansibleworks.com/docs/intro_installation.html) is installed on your `Control Machine`
* Setup your configuration file:
  ** `$ cp provisioning/group_vars/all.yml.example provisioning/group_vars/all.yml`
  ** Modify `provisioning/group_vars/all.yml` with your file versions, users, etc.

##### Remote Nodes:

* No root access
* sudo from a non-privileged user account (e.g., `vagrant`) to `sysadmin` account
* `Python 2.4+` is in `$PATH` and has the `simplejson` module (ansible requirements for your remote servers)
* OR `Python 2.6+` is installed and accessible via `$PATH`
* Perl 5+ is installed and accessible via `$PATH`
* gcc & make are accessible

# Development / Testing with Vagrant:

### Vagrant Configuration Assumptions:

1. [Virtualbox](https://www.virtualbox.org/wiki/Downloads) is installed
2. [Vagrant](http://vagrantup.com/) is installed
3. `vagrant.vm` maps to `33.33.33.10` (in your `/etc/hosts` file)

### Download the SUPPORT customized Vagrant box:

**Note**: Vagrant won't untar the SUPPORT box file currently, do the following steps manually:

```bash
$ wget http://bit.ly/SUPPORT-x64 -O
~/.vagrant/boxes/vagrant-centos59-x86_64-SUPPORT.box
$ cd ~/.vagrant/boxes
$ mkdir vagrant-centos59-x86_64-SUPPORT
$ tar -xzvf vagrant-centos59-x86_64-SUPPORT.box -C
vagrant-centos59-x86_64-SUPPORT/
$ vagrant box list
#=> vagrant-centos59-x86_64-SUPPORT
```

**Note**: To install the `python-simplejson` module for Python 2.4.3 on the SUPPORT VM run the following playbook:  
`ansible-playbook provisioning/init.yml -i provisioning/hosts/vagrant --user=vagrant --sudo`

### Develop / Test the Ansible Provisioning Playbook:

```bash
# --no-provision avoids an error for missing python-simplejson module for ansible
$ vagrant up --no-provision
# Boostrap the server to add python-simplejson
$ ansible-playbook provisioning/init.yml -i provisioning/hosts/vagrant --user=vagrant --sudo
# Repeat the following with each `provisioning/site.yml` modification:
$ vagrant provision
# Destroy as needed and repeat from `vagrant up`:
$ vagrant destroy
```
