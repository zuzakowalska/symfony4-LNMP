# -*- mode: ruby -*-
# vi: set ft=ruby :

PROJECT = 'symfony4-box'

VAGRANTFILE_API_VERSION = 2

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|

  config.vm.define PROJECT do |xenial|

    xenial.vm.box = "bento/ubuntu-16.04"
    xenial.vm.box_check_update = true

    xenial.vm.network "private_network", ip: "192.168.100.100"
    xenial.vm.network :forwarded_port, guest: 80, host: 8000, auto_correct: true
    xenial.vm.network :forwarded_port, guest: 443, host: 8443, auto_correct: true
    xenial.vm.network :forwarded_port, guest: 3306, host: 3306, auto_correct: true


    xenial.vm.hostname = PROJECT

    xenial.vm.provider "virtualbox" do |vb|

      vb.name = PROJECT
      vb.memory = "1024"
    end

    xenial.vm.provision "ansible" do |ansible|

        ansible.groups = {
            "symfony" => PROJECT
        }
        ansible.playbook = "ansible/playbook.yml"
        # ansible.verbose = "vvv"
     end
  end
  config.vm.synced_folder ".", "/vagrant/code/", type: "virtualbox"
  config.vm.synced_folder ".", "/vagrant", disabled: true
end
