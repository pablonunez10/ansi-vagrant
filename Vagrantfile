# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/xenial64"

    config.vm.provider "virtualbox" do |vb|
      vb.gui = true
      vb.memory = "2048"
      vb.name= "prueba"
  end

    config.vm.network "public_network", :bridge => "en0: Wi-Fi (Airport)", :ip => "192.168.32.79"
    config.vm.synced_folder "shared" , "/Prueba/shared"
    config.vm.provision "shell", path: "shared/config-ansible.sh"
    
    config.vm.synced_folder ".", "/vagrant"
    config.vm.provision "shell", inline: <<-SHELL
    apt-get update
    apt-get install -y nginx
    sed -i -e 's/\\/var\\/www\\/html/\\/vagrant/g' /etc/nginx/sites-enabled/default
    systemctl restart nginx
  SHELL
  
end
