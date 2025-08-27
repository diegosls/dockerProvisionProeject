# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.box = "debian/bookworm64"
  config.ssh.insert_key = false
  config.vm.hostname = "diego.igor"
  config.vm.network "private_network", ip: "192.168.56.145"
  
  # Sincronizar pasta local com a VM (para o docker-compose.yml)
  config.vm.synced_folder ".", "/vagrant", disabled: false
  
  config.vm.provider :virtualbox do |v|
    v.memory = 1024
    v.check_guest_additions = false
  end

  if Vagrant.has_plugin?("vagrant-vbguest")
    config.vbguest.auto_update = false
  end

  # Run Ansible *inside* the guest
  config.vm.provision "ansible_local" do |ansible|
    ansible.playbook = "playbook_ansible.yml"
    ansible.verbose = "v"
  end
end