# -*- mode: ruby -*-
# vi: set ft=ruby :

# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  # All Vagrant configuration is done here. The most common configuration
  # options are documented and commented below. For a complete reference,
  # please see the online documentation at vagrantup.com.

  config.omnibus.chef_version = :latest

  # Every Vagrant virtual environment requires a box to build off of.
  config.vm.box = "precise64"
  config.vm.box_url = "http://files.vagrantup.com/precise64.box"

  # Disable automatic box update checking. If you disable this, then
  # boxes will only be checked for updates when the user runs
  # `vagrant box outdated`. This is not recommended.
  # config.vm.box_check_update = false

  # Create a forwarded port mapping which allows access to a specific port
  # within the machine from a port on the host machine. In the example below,
  # accessing "localhost:8080" will access port 80 on the guest machine.
  config.vm.network "forwarded_port", guest: 80, host: 8181

  # user service
  config.vm.network "forwarded_port", guest: 3010, host: 3010

  # catalog service
  config.vm.network "forwarded_port", guest: 3020, host: 3020

  # cart/checkout service
  config.vm.network "forwarded_port", guest: 3030, host: 3030

  # orders service
  config.vm.network "forwarded_port", guest: 3040, host: 3040

  # inventory service
  config.vm.network "forwarded_port", guest: 3050, host: 3050

  # rabbitmq
  config.vm.network "forwarded_port", guest: 15672, host: 15672

  # Create a private network, which allows host-only access to the machine
  # using a specific IP.
  # config.vm.network "private_network", ip: "192.168.33.10"

  # Create a public network, which generally matched to bridged network.
  # Bridged networks make the machine appear as another physical device on
  # your network.
  # config.vm.network "public_network"

  # If true, then any SSH connections made will enable agent forwarding.
  # Default value: false
  config.ssh.forward_agent = true

  # Share an additional folder to the guest VM. The first argument is
  # the path on the host to the actual folder. The second argument is
  # the path on the guest to mount the folder. And the optional third
  # argument is a set of non-required options.
  config.vm.synced_folder "../web", "/web"

  # Provider-specific configuration so you can fine-tune various
  # backing providers for Vagrant. These expose provider-specific options.
  # Example for VirtualBox:
  #
  config.vm.provider "virtualbox" do |vb|
    # Don't boot with headless mode
    # vb.gui = true
  
    # Use VBoxManage to customize the VM. For example to change memory:
    vb.customize ["modifyvm", :id, "--memory", "2048"]
  end

  # Enable provisioning with chef solo, specifying a cookbooks path, roles
  # path, and data_bags path (all relative to this Vagrantfile), and adding
  # some recipes and/or roles.
  #
  config.vm.provision "chef_solo" do |chef|
    chef.add_recipe "apt"
    chef.add_recipe "build-essential"

    chef.add_recipe "ruby_build"
    chef.add_recipe "rbenv::user"
    chef.add_recipe "rbenv::vagrant"

    chef.add_recipe "memcached"
    chef.add_recipe "nginx"

    chef.add_recipe "nodejs"
    chef.add_recipe "nodejs::npm"

    chef.add_recipe "mysql::server"
    chef.add_recipe "mysql::client"

    chef.add_recipe "rabbitmq::default"
    chef.add_recipe "rabbitmq::mgmt_console"

    chef.add_recipe "httpie"

    chef.json = {
      'mysql' => {
        'server_root_password' => 'root',
        'server_debian_password' => 'vagrant',
        'server_repl_password' => 'root',
        'allow_remote_root' => true,

        'client' => {
          'packages' => ['mysql-client', 'libmysqlclient-dev', 'ruby-mysql']
        }
      },

      'rbenv' => {
        'user_installs' => [
          {
            'user' => 'vagrant',
            'rubies' => ['2.1.0'],
            'global' => '2.1.0'
          }
        ]
      },

      'nodejs' => {
        'npm' => '2.1.15'
      }
    }
  end
end
