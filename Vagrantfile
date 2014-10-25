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

    mkdir Desktop
    wget https://gist.githubusercontent.com/michalsanger/f141149da76c7074940c/raw/21bea79b271aef326fc27d5c5ca842d32e3b6dbb/Ubuntu_Unit_Terminal_launcher -O /home/vagrant/Desktop/terminal.desktop
    chmod u+x /home/vagrant/Desktop/terminal.desktop
    sudo chown -R vagrant:vagrant Desktop

    mkdir /home/vagrant/.config
    mkdir -p "/home/vagrant/.config/sublime-text-2/Installed Packages/"
    wget https://github.com/SiebelsTim/hack-sublime/blob/master/Hack.sublime-package?raw=true -O "/home/vagrant/.config/sublime-text-2/Installed Packages/Hack.sublime-package"
    sudo chown -R vagrant:vagrant /home/vagrant/.config
    
    sudo apt-get autoremove -y
  shell

end
