# -*- mode: ruby -*-
# vi: set ft=ruby :

# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = "2"


Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.box = "ubuntu/trusty64"
  config.vm.provider "virtualbox" do |v|
    v.memory = 2048
    v.cpus = 1
  end

#  config.vm.network "forwarded_port", guest: 3000, host: 3000
  config.ssh.forward_agent = true
  config.vm.hostname = "go-dev"

  # install golang tools
  config.vm.provision :shell, :inline => "wget https://storage.googleapis.com/golang/go1.4.2.linux-amd64.tar.gz"
  config.vm.provision :shell, :inline => "tar -C /usr/local -xzf go1.4.2.linux-amd64.tar.gz"
  config.vm.provision :shell, :inline => "rm go1.4.2.linux-amd64.tar.gz"
  config.vm.provision :shell, :inline => "mkdir -p /home/vagrant/projects/golang/src", :privileged => false

  # install tools
  config.vm.provision :shell, :inline => "apt-get -y install git"

  # Add github to the known_hosts so we can clone
  config.vm.provision :shell, :inline => "touch /home/vagrant/.ssh/known_hosts", :privileged => false
  config.vm.provision :shell, :inline => "ssh-keyscan -H github.com >> /home/vagrant/.ssh/known_hosts", :privileged => false
  config.vm.provision :shell, :inline => "chmod 600 /home/vagrant/.ssh/known_hosts", :privileged => false

  # setup zsh
  config.vm.provision :shell, :inline => "apt-get -y install zsh"
  config.vm.provision :shell, :inline => "chsh -s `which zsh` vagrant"

  # install my dotfiles.
  config.vm.provision :shell, :inline => "git clone git@github.com:pneisen/dotfiles.git", :privileged => false
  config.vm.provision :shell, :inline => "export SHELL=`which zsh` && /home/vagrant/dotfiles/setup.sh", :privileged => false
  config.vm.provision :shell, :inline => "rm -rf /home/vagrant/dotfiles_old", :privileged => false

end
