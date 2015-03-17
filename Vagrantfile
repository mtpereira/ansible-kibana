# -*- mode: ruby -*-
# vi: set ft=ruby ts=2 sw=2 tw=0 et :

vmname = File.basename(File.expand_path(File.dirname(__FILE__)))

Vagrant.configure("2") do |config|
  config.vm.define vmname do |ap|
    ap.vm.box = "opscode-ubuntu-14.04"
    ap.vm.box_url = "http://opscode-vm-bento.s3.amazonaws.com/vagrant/virtualbox/opscode_ubuntu-14.04_chef-provisionerless.box"
    ap.vm.hostname = vmname

    ap.vm.provider "virtualbox" do |v|
      v.customize ["modifyvm", :id, "--cpuexecutioncap", "50"]
      v.customize ["modifyvm", :id, "--memory", 256]
    end

    ap.vm.network :private_network, ip: "10.0.0.51"

    ap.vm.provision :ansible do |ansible|
      ansible.playbook = "test.yml"
      ansible.verbose = "vv"
    end
  end
end
