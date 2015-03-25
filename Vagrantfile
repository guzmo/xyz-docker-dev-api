# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure(2) do |config|
  config.vm.box = "ubuntu/trusty64"
  config.vm.network :forwarded_port, guest: 80, host: 7070
  config.vm.network :forwarded_port, guest: 3232, host: 3232
  config.vm.network :forwarded_port, guest: 27017, host: 27017

# deploy as services
 config.vm.provision :shell, path: 'docker-compose.sh', privileged: false
 config.vm.provision "shell", inline: "cd /vagrant && docker-compose up -d"
end
