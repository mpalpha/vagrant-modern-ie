# -*- mode: ruby -*-
# vi: set ft=ruby :

=begin
ModernIE VMs
edge-Win10
IE11-Win7
IE11-Win8.1
IE10-Win7
IE10-Win8
IE9-Win7
IE8-Win7
IE7-Vista
System Account Credentials
Username: IEUser
Password: Passw0rd!
=end

boxes = [
  {:name => "edge-Win10", :box => "modernIE/w10-edge"},
  {:name => "IE11-Win7", :box => "modernIE/w7-ie11"},
  {:name => "IE11-Win8.1", :box => "modernIE/w8.1-ie11"},
  {:name => "IE10-Win7", :box => "modernIE/w7-ie10"},
  {:name => "IE10-Win8", :box => "modernIE/w8-ie10"},
  {:name => "IE9-Win7", :box => "modernIE/w7-ie9"},
  {:name => "IE8-Win7", :box => "modernIE/w7-ie8"},
  {:name => "IE7-Vista", :box => "modernIE/vista-ie7"}
]

Vagrant.configure(2) do |config|
  boxes.each do |box|
    # If the box is win7-ie11, the convention for the box name is modern.ie/win7-ie11
    config.vm.box = box[:box]

    # big timeout since windows boot is very slow
    config.vm.boot_timeout = 500

    config.vm.guest = :windows
    config.vm.communicator = "winrm"
    config.winrm.username = "IEUser"
    config.winrm.password = "Passw0rd!"

    # redirect 127.0.0.1 to host ip(10.0.0.3) for windows8+ VM
    config.vm.provision "shell", inline: <<-SHELL
      netsh.exe interface portproxy add v4tov4 8000 10.0.0.3
    SHELL

    config.vm.synced_folder ".", "/vagrant", id: "vagrant-root", disabled: true
    config.vm.define box[:name], autostart: false do |machine|
      machine.vm.box = box[:box]
      config.vm.provider "virtualbox" do |vb|
        vb.customize ["modifyvm", :id, "--memory", "1024"]
        vb.customize ["modifyvm", :id, "--vram", "128"]
        vb.customize ["modifyvm", :id, "--cpus", "2"]
        vb.customize ["modifyvm", :id, "--ioapic", "on"]
        vb.customize ["modifyvm", :id, "--natnet1", "10.0.0.0/24"]
        vb.customize ["modifyvm", :id, "--natdnsproxy1", "on"]
        vb.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
        vb.customize ["guestproperty", "set", :id, "/VirtualBox/GuestAdd/VBoxService/--timesync-set-threshold", 10000]
        vb.gui = true
      end
    end
  end
end
