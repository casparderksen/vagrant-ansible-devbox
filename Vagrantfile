# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.box = "centos7-ansible"

  # Create a private network (IP must match IP used in ansible/local.yml)
  config.vm.network "private_network", ip: "192.168.33.10"

  # Web server
  config.vm.network :forwarded_port, guest: 80, host: 80
  config.vm.network :forwarded_port, guest: 443, host: 443

  # Java apps
  config.vm.network :forwarded_port, guest: 5005, host: 5005
  config.vm.network :forwarded_port, guest: 8080, host: 8080
  config.vm.network :forwarded_port, guest: 8443, host: 8443

  # Oracle Net Listener port
  config.vm.network :forwarded_port, guest: 1521, host: 1521

  # Weblogic AdminServer ports
  config.vm.network :forwarded_port, guest: 7001, host: 7001
  config.vm.network :forwarded_port, guest: 7002, host: 7002

  # Weblogic managed servers ports
  config.vm.network :forwarded_port, guest: 7011, host: 7011
  config.vm.network :forwarded_port, guest: 7012, host: 7012

  # CNTLM proxy
  config.vm.network :forwarded_port, guest: 3128, host: 3128

  # miniDC/OS (mapped from one DC/OS master port)
  config.vm.network :forwarded_port, guest: 8888, host: 8888


  # VirtualBox provider configuration
  config.vm.provider "virtualbox" do |vb|
    vb.name = "CentOS 7"
    vb.memory = "10240"
    vb.cpus = 2
  end

  # Mount projects folder
#  config.vm.synced_folder "D:/projects", "/home/vagrant/projects",
#    owner: "vagrant",
#    group: "vagrant",
#    mount_options: ["dmode=775,fmode=664"]

  # Mount /ansible folder (read-only for world)
#  config.vm.synced_folder "ansible", "/ansible",
#    owner: "vagrant",
#    group: "vagrant",
#    mount_options: ["dmode=775,fmode=664"]

  # Perform Ansible provisioning
  config.vm.provision "ansible_local" do |ansible|
    ansible.playbook = "devbox.yml"
    ansible.config_file = "ansible.cfg"
    ansible.provisioning_path = "/vagrant/ansible"
  end

end
