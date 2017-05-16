# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|

  config.vm.provider :virtualbox do |v|
    # On VirtualBox, we don't have guest additions or a functional vboxsf
    # in CoreOS, so tell Vagrant that so it can be smarter.
    v.check_guest_additions = false
    v.functional_vboxsf     = false
  end

  config.vm.provider 'virtualbox' do |v|
      v.linked_clone = true
  end

  # plugin conflict
  if Vagrant.has_plugin?("vagrant-vbguest") then
    config.vbguest.auto_update = false
  end

  config.vm.network "forwarded_port", guest: 80, host: 8080
  config.vm.network "forwarded_port", guest: 443, host: 8443

  # disable sync of local dir to /vagrant
  config.vm.synced_folder ".", "/vagrant", disabled: true

  config.vm.box = "coreos-stable"
  config.vm.box_url = "https://storage.googleapis.com/stable.release.core-os.net/amd64-usr/current/coreos_production_vagrant.json"

  config.vm.provision "ansible" do |ansible|
    ansible.playbook = "ansible/bootstrap.yaml"
    ansible.extra_vars = {
    ansible_ssh_user:"core",
    ansible_python_interpreter:"/home/core/bin/python"
    }
  end

  config.vm.provision "ansible" do |ansible2|
    ansible2.playbook = "ansible/playbook.yaml"
    ansible2.extra_vars = {
    ansible_ssh_user:"core",
    ansible_python_interpreter:"/home/core/bin/python"
    }
  end

end
