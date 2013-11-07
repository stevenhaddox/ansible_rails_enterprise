#Vagrant::Config.run do |config|
Vagrant.configure("2") do |config|
  config.vm.box = "vagrant-centos59-x86_64-SUPPORT"
  config.vm.box_url = "http://bit.ly/SUPPORT-x64"

  config.vm.network "private_network", ip: "33.33.33.10"

  config.vm.synced_folder ".", "/vagrant", disabled: true

  config.vm.provision :ansible do |ansible|
    ansible.verbose        = 'vv' # vv, vvv, false
    ansible.playbook       = "provisioning/playbook.yml"
    ansible.inventory_path = "provisioning/hosts_vagrant"
    ansible.sudo           = true
    ansible.sudo_user      = "sysadmin"
  end
end
