# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.box = "hashicorp/precise64"

  # config.vm.network :forwarded_port, guest: 80, host: 8080
  # config.vm.network :forwarded_port, guest: 8000, host: 8100
  # config.vm.network :private_network, ip: "192.168.66.66"

  config.vm.provider :virtualbox do |vb|
    vb.name = "HHVM Desktop"
    vb.customize ["modifyvm", :id, "--memory", "4096"]
    vb.customize ["modifyvm", :id, "--ostype", "Ubuntu_64"]
    vb.gui = true
  end
  
  config.vm.provision "file", source: "terminal.desktop", destination: "/home/vagrant/Desktop/terminal.desktop"

  config.vm.provision "shell", inline: <<-shell
    sudo apt-get update
    sudo apt-get install htop git -y --force-yes

    sudo apt-get install software-properties-common python-software-properties -y --force-yes
    sudo add-apt-repository ppa:mapnik/boost -y
    wget -O - http://dl.hhvm.com/conf/hhvm.gpg.key | sudo apt-key add -
    echo deb http://dl.hhvm.com/ubuntu precise main | sudo tee /etc/apt/sources.list.d/hhvm.list
    sudo apt-get update
    sudo apt-get install hhvm -y --force-yes

    sudo apt-get install ubuntu-desktop -y --force-yes
    sudo apt-get -y purge ubuntuone* libreoffice* thunderbird ubuntu-docs ibus-pinyin gnome-user-guide samba*

    sudo add-apt-repository ppa:webupd8team/sublime-text-2 -y
    sudo apt-get update
    sudo apt-get install sublime-text -y --force-yes

    mkdir -p "/home/vagrant/.config/sublime-text-2/Installed Packages/"
    mkdir /tmp/hack-sublime
    git clone https://github.com/SiebelsTim/hack-sublime.git /tmp/hack-sublime
    cp /tmp/hack-sublime/Hack.sublime-package "/home/vagrant/.config/sublime-text-2/Installed Packages/Hack.sublime-package"
    rm -rf /tmp/hack-sublime
    
    sudo chown -R vagrant:vagrant /home/vagrant/.config
    sudo chown -R vagrant:vagrant Desktop
    
    sudo apt-get autoremove -y
  shell



end
