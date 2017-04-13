# -*- mode: ruby -*-
# vi: set ft=ruby :

boxes = [
  {:name => :'zk01',:ip => '10.0.0.10',:cpus =>1,:mem =>512,:port =>19090,},
  {:name => :'zk02',:ip => '10.0.0.11',:cpus =>1,:mem =>512,:port =>29090,},
  {:name => :'zk03',:ip => '10.0.0.12',:cpus =>1,:mem =>512,:port =>39090,},
  ]

  #VAGRANTFILE_API_VERSION = "2"
  Vagrant.configure("2") do |config|
    boxes.each do |opts|
      config.vm.define opts[:name] do |config|
        config.vm.box = "ubuntu-16.04"
        config.vm.box_check_update = false
        config.vm.boot_timeout = 360
        config.ssh.username = 'vagrant'
        config.ssh.password = 'vagrant'
        config.vm.synced_folder ".","/vagrant",disabled: true
        #config.vm.network "public_network"
        config.vm.network "private_network",ip:opts[:ip]
	config.vm.network :forwarded_port,guest:9090,host:opts[:port]
        #,ip:opts[:ip],bridge:"enp2s0"
        config.vm.hostname = "%s.vagrant"% opts[:name].to_s
        config.vm.provider "virtualbox" do |vb|
          vb.customize ["modifyvm",:id,"--cpus",opts[:cpus]] if [opts[:cpus]]
          vb.customize ["modifyvm",:id,"--memory",opts[:mem]] if [opts[:mem]]
        end
	#config.vm.provision "shell", inline: <<-SHELL
         # sudo su -
         # mkdir /etc/yum.repos.d/repo.bak
         # mv /etc/yum.repos.d/*.repo /etc/yum.repos.d/repo.bak/
         # wget http://mirrors.163.com/.help/CentOS7-Base-163.repo -P /etc/yum.repos.d/
         # yum clean all && sudo yum makecache
#	SHELL
    #config.vm.provision "shell",path:"k8s_init.sh"
      end
    end
   # config.vm.provision "shell",path:"init.sh"
  end

















# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
#Vagrant.configure("2") do |config|
  # The most common configuration options are documented and commented below.
  # For a complete reference, please see the online documentation at
  # https://docs.vagrantup.com.

  # Every Vagrant development environment requires a box. You can search for
  # boxes at https://atlas.hashicorp.com/search.
  #config.vm.box = "centos7"

  # Disable automatic box update checking. If you disable this, then
  # boxes will only be checked for updates when the user runs
  # `vagrant box outdated`. This is not recommended.
  # config.vm.box_check_update = false

  # Create a forwarded port mapping which allows access to a specific port
  # within the machine from a port on the host machine. In the example below,
  # accessing "localhost:8080" will access port 80 on the guest machine.
  # config.vm.network "forwarded_port", guest: 80, host: 8080

  # Create a private network, which allows host-only access to the machine
  # using a specific IP.
  # config.vm.network "private_network", ip: "192.168.33.10"

  # Create a public network, which generally matched to bridged network.
  # Bridged networks make the machine appear as another physical device on
  # your network.
  # config.vm.network "public_network"

  # Share an additional folder to the guest VM. The first argument is
  # the path on the host to the actual folder. The second argument is
  # the path on the guest to mount the folder. And the optional third
  # argument is a set of non-required options.
  # config.vm.synced_folder "../data", "/vagrant_data"

  # Provider-specific configuration so you can fine-tune various
  # backing providers for Vagrant. These expose provider-specific options.
  # Example for VirtualBox:
  #
  # config.vm.provider "virtualbox" do |vb|
  #   # Display the VirtualBox GUI when booting the machine
  #   vb.gui = true
  #
  #   # Customize the amount of memory on the VM:
  #   vb.memory = "1024"
  # end
  #
  # View the documentation for the provider you are using for more
  # information on available options.

  # Define a Vagrant Push strategy for pushing to Atlas. Other push strategies
  # such as FTP and Heroku are also available. See the documentation at
  # https://docs.vagrantup.com/v2/push/atlas.html for more information.
  # config.push.define "atlas" do |push|
  #   push.app = "YOUR_ATLAS_USERNAME/YOUR_APPLICATION_NAME"
  # end

  # Enable provisioning with a shell script. Additional provisioners such as
  # Puppet, Chef, Ansible, Salt, and Docker are also available. Please see the
  # documentation for more information about their specific syntax and use.
  # config.vm.provision "shell", inline: <<-SHELL
  #   apt-get update
  #   apt-get install -y apache2
  # SHELL
#end
