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
    # Define a trigger to run before the any provisioner
    master.trigger.before :provisioner_run, type: :hook do |trigger|
      trigger.info = "Retrieving the IP address of the machine"
      trigger.ruby do |env, machine|
        $ip_address = `utmctl ip-address #{machine.id} | head -n 1 > playbooks/ip_address && cat playbooks/ip_address`.lines.first.strip
        puts "The IP address of the machine is: #{$ip_address}"
      end
    end


    master.vm.provision "ansible" do |ansible|
      ansible.compatibility_mode = "2.0"
      ansible.playbook = "playbooks/master-playbook.yml"
      ansible.extra_vars = {
        node_ip: "{{ lookup('file', 'ip_address') }}",
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
      end
    end
  end
end