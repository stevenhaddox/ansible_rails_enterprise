# Ansible Rails Enterprise Provisioner

### Environment Assumptions:

##### Control Machine:

* [Ansible](http://www.ansibleworks.com/docs/intro_installation.html) is installed on your `Control Machine`
* Setup your configuration file:
  *     `$ cp provisioning/group_vars/all.yml.example provisioning/group_vars/all.yml`
  * Modify `provisioning/group_vars/all.yml` with your file versions, users, etc.
  * Download all src files needed to: `provisioning/src_files`

##### Remote Nodes:

* No root access
* sudo from a non-privileged user account (e.g., `vagrant`) to `sysadmin` account
* `Python 2.6+` is installed and accessible via `$PATH`
* OR `Python 2.4+` is in `$PATH` and has the `simplejson` module (ansible requirements for your remote servers)
* Perl 5+ is installed and accessible via `$PATH`
* gcc & make are accessible

### Variables:

The following files have variables with defaults you'll probably want to modify:

* Site vars: `provisioning/group_vars/all.yml`
* Package vars: `provisioning/group_vars/src.yml`
* httpd: `provisioning/roles/web/vars/main.yml`

# Development / Testing with Vagrant:

### Vagrant Configuration Assumptions:

1. [Virtualbox](https://www.virtualbox.org/wiki/Downloads) is installed
2. [Vagrant](http://vagrantup.com/) is installed
3. `vagrant.vm` maps to `33.33.33.10` (in your `/etc/hosts` file)

### Download the SUPPORT customized Vagrant box:

**Note**: Vagrant won't untar the SUPPORT box file currently, do the following steps manually:

```bash
$ wget http://bit.ly/SUPPORT-x64 -O
~/.vagrant.d/boxes/vagrant-centos59-x86_64-SUPPORT.box
$ cd ~/.vagrant.d/boxes
$ mkdir vagrant-centos59-x86_64-SUPPORT
$ tar -xzvf vagrant-centos59-x86_64-SUPPORT.box -C
vagrant-centos59-x86_64-SUPPORT/
$ vagrant box list
#=> vagrant-centos59-x86_64-SUPPORT
```

**Note**: To install the `python-simplejson` module for Python 2.4.3 on the SUPPORT VM run the following playbook:  
`ansible-playbook provisioning/init.yml -i provisioning/hosts/vagrant --u vagrant --sudo`

### Develop / Test the Ansible Provisioning Playbook:
Make sure your ssh key has been added to the VMs authorized keys before attempting to provision

```bash
# Spin-up the VM and bootstrap the server to add python-simplejson & needed packages
$ vagrant up --no-provision && ansible-playbook provisioning/init.yml -i provisioning/hosts/vagrant -u vagrant -s
# Repeat the following with each `provisioning/site.yml` modification:
$ ansible-playbook -i provisioning/hosts/vagrant provisioning/site.yml -u vagrant -s
# Destroy as needed and repeat from `vagrant up`:
$ vagrant destroy
```


[![Bitdeli Badge](https://d2weczhvl823v0.cloudfront.net/stevenhaddox/ansible_rails_enterprise/trend.png)](https://bitdeli.com/free "Bitdeli Badge")

