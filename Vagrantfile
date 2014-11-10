# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|

  config.vm.box = "ubuntu-12.04-64-puppet"
  config.vm.box_url = "https://vagrantcloud.com/puppetlabs/boxes/ubuntu-12.04-64-puppet/versions/1/providers/virtualbox.box"

  # config.vm.provider :virtualbox do |vb|
  #   vb.customize ["modifyvm", :id, "--ioapic", "on"]
  #   vb.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
  #   vb.memory = 2048
  #   vb.cpus = 2
  # end

  config.vm.network :forwarded_port, host: 8880, guest: 8080
  config.vm.network :forwarded_port, host: 8843, guest: 8443
  config.vm.network :forwarded_port, host: 8822, guest: 8022
  config.vm.network :forwarded_port, host: 8887, guest: 8787
  config.vm.network :forwarded_port, host: 27016, guest: 27017

  # need to install vagrant-proxyconf:
  # vagrant plugin install vagrant-proxyconf
  config.proxy.http     = "http://localhost:3128"
  config.proxy.https    = "http://localhost:3128"
  config.proxy.no_proxy = "localhost,127.0.0.1"

  # Use puppet provisionner to configure everything else
  config.vm.provision :puppet do |puppet|
    puppet.manifests_path = "manifests"
    puppet.module_path = "modules"
    puppet.manifest_file  = "vagrant-opal.pp"
    puppet.options = "-v"
    puppet.facter = { "vagrant_box" => true }
  end

end
