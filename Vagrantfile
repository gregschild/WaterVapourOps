# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|

  config.vm.define "app" do |app|
    app.vm.box = "bento/ubuntu-16.04"
    app.vm.synced_folder "webserver/", "/root/servers/webserver"
    app.vm.synced_folder "../app", "/var/www/html"
    app.vm.provision "shell", path: "webserver/provision.sh"
    app.vm.provision "shell", inline: "sudo usermod -a -G www-data vagrant"
    app.vm.network :forwarded_port, guest: 80, host: 3000
  end

  config.vm.define "api" do |api|
    api.vm.box = "bento/ubuntu-16.04"
    api.vm.synced_folder "webserver/", "/root/servers/webserver"
    api.vm.synced_folder "../api", "/var/www/html"
    api.vm.provision "shell", path: "webserver/provision.sh"
    api.vm.provision "shell", inline: "sudo usermod -a -G www-data vagrant"
    api.vm.network :forwarded_port, guest: 80, host: 3001
  end

  config.vm.define "db" do |db|
    db.vm.box = "bento/ubuntu-16.04"
    db.vm.synced_folder "database/", "/root/servers/database"
    db.vm.provision "shell", path: "database/provision.sh"
  end
end
