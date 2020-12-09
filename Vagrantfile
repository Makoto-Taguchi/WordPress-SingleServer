# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  # Ansible
  provision_config = {
    :playbook => "site.yml",
    :inventory_path => "inventory/hosts",
    :verbose => "v"
  }

  # Master DB
  config.vm.define "wp-server" do |vm01|
    vm01.vm.hostname = "wp-server"
    vm01.vm.box = "centos/7"
    vm01.vm.provider "virtualbox" do |vb|
      vb.memory = "1024"
    end
    vm01.vm.network "private_network", ip: "192.168.56.50", auto_config: false
    vm01.vm.network :forwarded_port, id: "ssh", host: 2230, guest: 22
    vm01.vm.provision :ansible, provision_config.merge(:limit => "wp-server")
    # vm01.vm.synced_folder "./htdocs", "/var/www/html", :mount_options => [ "dmode=777", "fmode=755" ]
    vm01.vm.synced_folder "./htdocs", "/var/www/html", type: "nfs", :mount_options  => ['nolock,vers=3,udp']
  end

end
