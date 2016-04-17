# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure(2) do |config|

  # Standard configuration for all boxes
  # boxes at https://atlas.hashicorp.com/search.
  config.vm.box = "fedora/23-cloud-base"
  config.vm.synced_folder "./", "/vagrant", type: "rsync"

  config.vm.define :master do |ms|
    ms.vm.hostname = "kube-master"
    ms.vm.network :private_network, ip: "192.168.50.2", :libvirt__network_name => "kubernetes"
    ms.vm.provider :libvirt do |libvirt|
      libvirt.uri = "qemu+unix:///system"
      libvirt.driver = "kvm"
      libvirt.connect_via_ssh = false
      libvirt.username = "vagrant"
      libvirt.storage_pool_name = "default"
      libvirt.memory = 512
      libvirt.cpus = 1
      libvirt.machine_arch = "x86_64"
      libvirt.nested = false
    end
    ms.vm.provision :file, source: "ca.pem", destination: "ca.pem"    
    ms.vm.provision :file, source: "master-key.pem", destination: "master-key.pem"    
    ms.vm.provision :file, source: "master.pem", destination: "master.pem"    
    ms.vm.provision :file, source: "master.provision", destination: "provision.sh"    
    ms.vm.provision :file, source: "master.etcd", destination: "etcd.conf"    
    ms.vm.provision :shell do |shell|
      shell.inline = <<-SHELL
        sudo /bin/sh ~vagrant/provision.sh
      SHELL
    end
  end

  config.vm.define :node1 do |nd1|
    nd1.vm.hostname = "kube-node1"
    nd1.vm.network :private_network, ip: "192.168.50.3", :libvirt__network_name => "kubernetes"
    nd1.vm.provider :libvirt do |libvirt|
      libvirt.uri = "qemu+unix:///system"
      libvirt.driver = "kvm"
      libvirt.connect_via_ssh = false
      libvirt.username = "vagrant"
      libvirt.storage_pool_name = "default"
      libvirt.memory = 512
      libvirt.cpus = 1
      libvirt.machine_arch = "x86_64"
      libvirt.nested = false
    end
    nd1.vm.provision :file, source: "ca.pem", destination: "ca.pem"    
    nd1.vm.provision :file, source: "node1-key.pem", destination: "node1-key.pem"    
    nd1.vm.provision :file, source: "node1.pem", destination: "node1.pem"    
    nd1.vm.provision :file, source: "node1.provision", destination: "provision.sh"    
    nd1.vm.provision :file, source: "node1.etcd", destination: "etcd.conf"    
    nd1.vm.provision :shell do |shell|
      shell.inline = <<-SHELL
        sudo /bin/sh ~vagrant/provision.sh
      SHELL
    end
  end

  config.vm.define :node2 do |nd2|
    nd2.vm.hostname = "kube-node2"
    nd2.vm.network :private_network, ip: "192.168.50.4", :libvirt__network_name => "kubernetes"
    nd2.vm.provider :libvirt do |libvirt|
      libvirt.uri = "qemu+unix:///system"
      libvirt.driver = "kvm"
      libvirt.connect_via_ssh = false
      libvirt.username = "vagrant"
      libvirt.storage_pool_name = "default"
      libvirt.memory = 512
      libvirt.cpus = 1
      libvirt.machine_arch = "x86_64"
      libvirt.nested = false
    end
    nd2.vm.provision :file, source: "ca.pem", destination: "ca.pem"    
    nd2.vm.provision :file, source: "node2-key.pem", destination: "node2-key.pem"    
    nd2.vm.provision :file, source: "node2.pem", destination: "node2.pem"    
    nd2.vm.provision :file, source: "node2.provision", destination: "provision.sh"    
    nd2.vm.provision :file, source: "node2.etcd", destination: "etcd.conf"    
    nd2.vm.provision :shell do |shell|
      shell.inline = <<-SHELL
        sudo /bin/sh ~vagrant/provision.sh
      SHELL
    end
  end

end
