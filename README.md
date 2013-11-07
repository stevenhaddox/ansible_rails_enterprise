# Ansible Rails Enterprise Provisioner

### Environment Assumptions:

* No root access
* sudo from a non-privileged user account (e.g., `vagrant`) to `sysadmin` account
* `vagrant.vm` in your `/etc/hosts` maps to `33.33.33.10`
* [Virtualbox](https://www.virtualbox.org/wiki/Downloads) is installed
* `Python 2.4+` is in `$PATH` and has the `simplejson` module

**Note**: To install the `simplejson` module in `Python < 2.6` run the following:  
`ansible vagrant -i provisioning/hosts_vagrant -u vagrant --sudo -m raw -a "yum install -y python-simplejson"`

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

### Develop / Test the Ansible Provisioning Playbook:

```bash
# Start the vagrant VM:
$ vagrant up
# Run the ansible playbook:
$ vagrant provision
```
