# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure(2) do |config|
  config.vm.box = "ubuntu/trusty64"

  ssh_public_key = File.read(File.join(Dir.home, ".ssh", "id_rsa.pub"))

  config.vm.network "private_network", ip: "192.168.33.98"
  config.vm.hostname = "docker"

  config.vm.provision "shell", inline: <<-SHELL
    sudo apt-get update
    echo "#{ssh_public_key}" >> /home/vagrant/.ssh/authorized_keys
  SHELL

  config.vm.provision :ansible do |ansible|
    ansible.playbook = "install-docker.yml"
    ansible.verbose = "v"
  end
end

