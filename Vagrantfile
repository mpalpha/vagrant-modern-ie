# -*- mode: ruby -*-
# vi: set ft=ruby :

# auto install plugins
required_plugins = %w[vagrant-atomic]
required_plugins.each do |plugin|
  exec "sudo vagrant plugin install #{plugin};vagrant #{ARGV.join(' ')}" unless Vagrant.has_plugin? plugin || ARGV[0] == 'plugin'
end

info_heredoc = <<-HEREDOC
  ie8-win7
  ie9-win7
  ie10-win7
  ie11-win7
  ie11-win81
  msedge-win10
  System Account Credentials
  Username: IEUser
  Password: Passw0rd!
HEREDOC

# download the vagrant boxes from https://developer.microsoft.com/en-us/microsoft-edge/tools/vms/
boxes = [
  { name: 'ie8-win7', box: 'IE8 - Win7' },
  { name: 'ie9-win7', box: 'IE9 - Win7' },
  { name: 'ie10-win7', box: 'IE10 - Win7' },
  { name: 'ie11-win7', box: 'IE11 - Win7' },
  { name: 'ie11-win81', box: 'IE11 - Win81' },
  { name: 'msedge-win10', box: 'MSEdge - Win10' }
]

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.

Vagrant.configure('2') do |config|
  boxes.each do |box|
    # The most common configuration options are documented and commented below.
    # For a complete reference, please see the online documentation at
    # https://docs.vagrantup.com.

    # Every Vagrant development environment requires a box. You can search for
    # boxes at https://atlas.hashicorp.com/search.
    config.vm.box_url = box[:box]
    config.vm.box = box[:name]

    # configure SSH
    # config.ssh.forward_agent = false
    # config.ssh.insert_key = false
    config.ssh.username = 'IEUser'
    config.ssh.password = 'Passw0rd!'

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
    # config.vm.network "public_network", use_dhcp_assigned_default_route: true
    ### host ip is 10.0.2.2

    # Share an additional folder to the guest VM. The first argument is
    # the path on the host to the actual folder. The second argument is
    # the path on the guest to mount the folder. And the optional third
    # argument is a set of non-required options.
    # config.vm.synced_folder "../data", "/vagrant_data"

    config.vm.define box[:name], autostart: false do |machine|
      machine.vm.box = box[:name]
      # Provider-specific configuration so you can fine-tune various
      # backing providers for Vagrant. These expose provider-specific options.
      # Example for VirtualBox:
      #
      config.vm.provider 'virtualbox' do |vb|
        #   # Display the VirtualBox GUI when booting the machine
        vb.gui = true
        #
        #   # Customize the amount of memory on the VM:
        vb.memory = '1024'
        vb.customize ['modifyvm', :id, '--memory', '1024']
        vb.customize ['modifyvm', :id, '--vram', '128']
        vb.customize ['modifyvm', :id, '--cpus', '2']
        vb.customize ['modifyvm', :id, '--ioapic', 'on']
        vb.customize ['modifyvm', :id, '--natdnsproxy1', 'on']
        vb.customize ['modifyvm', :id, '--natdnshostresolver1', 'on']
      end
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
      config.vm.provision 'shell', privileged: false, inline: <<-HEREDOC
        echo "Vagrant Box #{box[:name]} is provisioned!"
        echo "#{info_heredoc}"
        echo "Local host IP address is http://10.0.2.2"
      HEREDOC
    end
  end
end
