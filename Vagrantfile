# -*- mode: ruby -*-
# vi: set ft=ruby :

IMAGE_NAME = "utm/bookworm"
N = 2

Vagrant.configure("2") do |config|

  config.vm.provider "utm" do |u|
    u.memory = 2048
    u.cpus = 2
  end
      
  config.vm.define "k8s-master" do |master|
    master.vm.box = IMAGE_NAME
    
    master.vm.hostname = "k8s-master"
    master.vm.provision "ansible" do |ansible|
      ansible.compatibility_mode = "2.0"
      ansible.playbook = "playbooks/master-playbook.yml"
      ansible.extra_vars = {
          node_ip: "192.168.75.108",
      }
    end
  end

  (1..N).each do |i|
    config.vm.define "node-#{i}" do |node|
      node.vm.box = IMAGE_NAME

      node.vm.hostname = "node-#{i}"
      node.vm.provision "ansible" do |ansible|
        ansible.compatibility_mode = "2.0"
        ansible.playbook = "playbooks/node-playbook.yml"
        ansible.extra_vars = {
            node_ip: "192.168.75.#{i + 108}",
        }
      end
    end
  end
end