# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.box = "debian/stretch64"

  config.vm.provider "virtualbox" do |vb|
    vb.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
    vb.customize ["modifyvm", :id, "--ioapic", "on"]
  end

  config.vm.define "vault" do |vault|
    vault.vm.hostname = "vault01"
    vault.vm.network :private_network, ip: "192.168.33.22"

    vault.vm.provider :virtualbox do |vb|
        vb.customize ["modifyvm", :id, "--memory", "256"]
        vb.customize ["modifyvm", :id, "--cpus", "1"]
    end

    vault.vm.provision "ansible" do |ansible|
      ansible.compatibility_mode = "2.0"
      ansible.playbook = "provisioning/vault.yml"
      ansible.inventory_path = "provisioning/inventory"
      ansible.become = true
    end
  end

  config.vm.define "ssh" do |ssh|
    ssh.vm.hostname = "ssh01"
    ssh.vm.network :private_network, ip: "192.168.33.23"

    ssh.vm.provider :virtualbox do |vb|
        vb.customize ["modifyvm", :id, "--memory", "256"]
        vb.customize ["modifyvm", :id, "--cpus", "1"]
    end

    ssh.vm.provision "ansible" do |ansible|
      ansible.compatibility_mode = "2.0"
      ansible.playbook = "provisioning/ssh.yml"
      ansible.inventory_path = "provisioning/inventory"
      ansible.become = true
    end
  end

  config.vm.define "es" do |es|
    es.vm.hostname = "es01"
    es.vm.network :private_network, ip: "192.168.33.24"

    es.vm.provider :virtualbox do |vb|
        vb.customize ["modifyvm", :id, "--memory", "1536"]
        vb.customize ["modifyvm", :id, "--cpus", "2"]
    end

    es.vm.provision "ansible" do |ansible|
      ansible.compatibility_mode = "2.0"
      ansible.playbook = "provisioning/es.yml"
      ansible.inventory_path = "provisioning/inventory"
      ansible.become = true
    end
  end

end
