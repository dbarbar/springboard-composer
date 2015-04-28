ip = '192.168.100.100'
name = 'localdev'
cpus = 2
memory = 1024
domain = springboard.local
docroot = www

Vagrant.configure(2) do |config|
  config.vm.box = "dbarbar/local-springboard"

  config.vm.network :private_network, ip: ip
  config.vm.hostname = name
  config.vm.synced_folder ".", "/vagrant", type: "nfs"
  config.vm.synced_folder docroot, "/docroot", type: "nfs"

  # VirtualBox
  config.vm.provider "virtualbox" do |v, override|
    v.name = name
    v.memory = memory
    v.cpus = cpus

    # Fix issue with DNS
    # @todo Is this still needed?
    v.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
    v.customize ["modifyvm", :id, "--natdnsproxy1", "on"]
  end

  # VMWare Fusion
  config.vm.provider "vmware_fusion" do |v, override|
    v.name = name
    v.memory = memory
    v.cpus = cpus
  end

  config.vm.provision "shell" do |s|
    s.path = "build/provision.sh"
    s.args = [domain]
  end

end
