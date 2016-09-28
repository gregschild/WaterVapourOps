# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|

  config.vm.define "test" do |test|
    test.vm.box = "bento/ubuntu-16.04"
    test.vm.hostname = "test"
    test.vm.synced_folder "cookbooks/", "/home/vagrant/cookbooks"
  end


  config.vm.define "app" do |app|
    app.vm.box = "bento/ubuntu-16.04"
    app.vm.hostname = "app"
    app.vm.synced_folder "webserver/", "/root/servers/webserver"
    app.vm.synced_folder "../app", "/var/www/html"
    app.vm.provision "shell", path: "webserver/provision.sh"
    app.vm.provision "shell", inline: "sudo usermod -a -G www-data vagrant"
    app.vm.network :private_network, ip: "192.10.10.100"
    app.vm.network :forwarded_port, guest: 80, host: 3000
  end

  config.vm.define "api" do |api|
    api.vm.box = "bento/ubuntu-16.04"
    api.vm.hostname = "api"
    api.vm.synced_folder "webserver/", "/root/servers/webserver"
    api.vm.synced_folder "../api", "/var/www/html"
    api.vm.provision "shell", path: "webserver/provision.sh"
    api.vm.provision "shell", inline: "sudo usermod -a -G www-data vagrant"
    api.vm.network :private_network, ip: "192.10.10.150"
    api.vm.network :forwarded_port, guest: 80, host: 3001
  end

  config.vm.define "db" do |db|
    db.vm.box = "bento/ubuntu-16.04"
    db.vm.hostname = "db"
    db.vm.synced_folder "database/", "/root/servers/database"
    db.vm.provision "shell", path: "database/provision.sh"
    db.vm.network :private_network, ip: "192.10.10.200"
  end
end
