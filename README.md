# Ansible Rails Enterprise Provisioner

### Environment Assumptions:

* No root access
* sudo from a non-privileged user account (e.g., `vagrant`) to `sysadmin` account
* `Python 2.4+` is in `$PATH` and has the `simplejson` module (ansible requirements for your remote servers)

---

# Development / Testing with Vagrant:

### Vagrant Configuration Assumptions:

* `vagrant.vm` maps to `33.33.33.10` (in your `/etc/hosts` file)
* [Virtualbox](https://www.virtualbox.org/wiki/Downloads) is installed

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

**Note**: To install the `simplejson` module on Python 2.4.3 on the SUPPORT VM run the following:  
`ansible vagrant -i provisioning/hosts_vagrant -u vagrant --sudo -m raw -a "yum install -y python-simplejson"`

### Develop / Test the Ansible Provisioning Playbook:

```bash
# Start the vagrant VM:
$ vagrant up
# Run the ansible playbook:
$ vagrant provision
```

### Repeat as Needed:

```bash
$ vagrant destroy
$ vagrant up
# Before your first provision
$ ansible vagrant -i provisioning/hosts_vagrant -u vagrant --sudo -m raw -a "yum install -y python-simplejson"
$ vagrant provision
```
