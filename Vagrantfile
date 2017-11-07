# -*- mode: ruby -*-
# vi: set ft=ruby :

=begin
ModernIE VMs
xp-ie8
w8-ie10
w8.1-ie11
w7-ie9
w7-ie10
w7-ie11
EdgeOnWindows10
System Account Credentials
Username: IEUser
Password: Passw0rd!
=end

boxes = [
  {:name => "xp-ie8",:box => "rogeriopradoj/xp-ie8"},
  {:name => "w8-ie10",:box => "rogeriopradoj/win8-ie10"},
  {:name => "w8.1-ie11",:box => "rogeriopradoj/win81-ie11"},
  {:name => "w7-ie9",:box => "getdigital/ie9-win7"},
  {:name => "w7-ie10",:box => "ferhaty/win7ie10winrm"},
  {:name => "w7-ie11",:box => "vitaminless/modern_ie11_win7_for_mac"},
  {:name => "EdgeOnWindows10",:box => "Microsoft/EdgeOnWindows10"},
]

Vagrant.configure(2) do |config|
  boxes.each do |box|
    # If the box is win7-ie11, the convention for the box name is modern.ie/win7-ie11
    # config.vm.box = "modernIE/#{box[:name]}"
    config.vm.box = box[:box]

    # If the box is vagrant-win10-msedge use alternative url
    # config.vm.box_url = "http://aka.ms/#{box[:box]}"

    # big timeout since windows boot is very slow
    config.vm.boot_timeout = 500
    config.vm.guest = :windows
    config.ssh.username = 'IEUser'
    config.ssh.password = 'Passw0rd!'

    config.vm.communicator = "winrm"
    config.winrm.username = "IEUser"
    config.winrm.password = "Passw0rd!"

    # redirect 127.0.0.1 to host ip(10.0.0.3) for windows8+ VM
    if box[:name] !~ /ie6|ie7/i
    config.vm.provision "shell", inline: <<-SHELL
      netsh.exe interface portproxy add v4tov4 3001 10.0.0.3
    SHELL
    end

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
