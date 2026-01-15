Vagrant.configure("2") do |config|

  # Base VM image
  config.vm.box = "debian/bookworm64"

  config.vm.define "anonimo" do |a|
    # Hostname
    config.vm.hostname = "mirror.sistema.sol"

    # Private network IP
    config.vm.network "private_network", ip: "192.168.56.10"

    # Run playbook automatically
    config.vm.provision "ansible" do |ansible|
      ansible.playbook = "./anonymous-server/playbook.yml"
    end
  end

  config.vm.box = "ubuntu/focal64"


  config.vm.define "ftpserver" do |s|
    s.vm.hostname = "ftpserver"
    s.vm.network "private_network", ip: "192.168.56.20"
    s.vm.provision "ansible" do |ansible|
      ansible.playbook = "./Server-Secure/playbook.yml"
    end
  end


end



