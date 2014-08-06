# -*- mode: ruby -*-
# vi: set ft=ruby :

# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
    config.vm.box = "c65lvm"
    config.vm.box_url = "http://vntx.cc/boxes/c65lvm_vmware.box"
    config.vm.provision "ansible" do |a|
        a.playbook = "jenkins.yaml"
        a.host_key_checking = false
        a.groups = { "launched" => ["default"] }
    end
end
