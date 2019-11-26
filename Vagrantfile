# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|

  config.vm.box = "centos/6"
  config.vm.provider :libvirt do |vb|
    vb.memory = 4096
    vb.cpus = "2"
  end

	config.vm.define "weechat" do |node|
		node.vm.synced_folder ".", "/vagrant", type: "sshfs"
		node.vm.hostname = "weechat.local"
		node.vm.network :private_network, ip: "10.0.15.30"
		node.vm.provision :hostmanager
		node.vm.provision :ansible do |ansible|
			ansible.playbook = "playbook.yml"
			ansible.compatibility_mode = "2.0"
			ansible.limit = "all"
		end
	end

	if Vagrant.has_plugin?("vagrant-hostmanager")
		config.hostmanager.enabled = false
		config.hostmanager.manage_host = true
		config.hostmanager.manage_guest = true
		config.hostmanager.include_offline = true
	end
end
