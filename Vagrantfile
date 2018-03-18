# -*- mode: ruby -*-
# vi: set ft=ruby :
# vi: set tabstop=2 :
# vi: set shiftwidth=2 :

Vagrant.configure("2") do |config|

  vms_freebsd = [
    { :name => "freebsd-11", :box => "freebsd/FreeBSD-11.1-STABLE",  :vars => {} },
    { :name => "freebsd-12", :box => "freebsd/FreeBSD-12.0-CURRENT", :vars => {} }
  ]

  config.vm.network "private_network", type: "dhcp"
  config.vm.synced_folder ".", "/vagrant", id: "vagrant-root", disabled: true

  vms_freebsd.each do |opts|
    config.vm.base_mac = "080027D14C66"
    config.vm.define opts[:name] do |m|
      m.vm.box = opts[:box]
      m.vm.provider "virtualbox" do |v, override|
        override.ssh.shell = "csh"
        v.cpus = 2
        v.memory = 512
      end
      m.vm.provision "shell", inline: "pkg install -y python bash"
      m.vm.provision "ansible" do |ansible|
        ansible.playbook = "tests/test.yml"
        ansible.verbose = 'vv'
        ansible.become = true
        ansible.extra_vars = opts[:vars].merge({ "ansible_python_interpreter": '/usr/local/bin/python' })
      end
    end
  end

end
