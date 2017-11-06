# -*- mode: ruby -*-
# vi: set ft=ruby :

=begin
ModernIE VMs
xp-ie6
xp-ie8
vista-ie7
win7-ie8
win7-ie9
win7-ie10
win7-ie11
win8-ie10
win81-ie11
win10-msedge
System Account Credentials
Username: IEUser
Password: Passw0rd!
=end

boxes = [
  {:name => "xp-ie6",:box => "vagrant-xp-ie6"},
  {:name => "xp-ie8",:box => "vagrant-xp-ie8"},
  {:name => "vista-ie7",:box => "vagrant-vista-ie7"},
  {:name => "win7-ie8",:box => "vagrant-win7-ie8"},
  {:name => "win7-ie9",:box => "vagrant-win7-ie9"},
  {:name => "win7-ie10",:box => "vagrant-win7-ie10"},
  {:name => "win7-ie11",:box => "vagrant-win7-ie11"},
  {:name => "win8-ie10",:box => "vagrant-win8-ie10"},
  {:name => "win81-ie11",:box => "vagrant-win81-ie11"},
  {:name => "win10-msedge",:box => "vagrant-win10-msedge"},
]

Vagrant.configure(2) do |config|
  boxes.each do |box|
    # If the box is win7-ie11, the convention for the box name is modern.ie/win7-ie11
    config.vm.box = "modern.ie/#{box[:box]}"

    # If the box is vagrant-win10-msedge use alternative url
    if box[:box]=="vagrant-win10-msedge"
      config.vm.box_url = "https://vagrantcloud.com/Microsoft/boxes/EdgeOnWindows10/versions/1.0/providers/virtualbox.box"
    else
      config.vm.box_url = "http://aka.ms/#{box[:box]}"
    end

    # big timeout since windows boot is very slow
    config.vm.boot_timeout = 500
    config.vm.guest = :windows
    config.vm.communicator = "winrm"
    config.winrm.username = "IEUser"
    config.winrm.password = "Passw0rd!"

    # redirect 127.0.0.1 to host ip(10.0.0.3) for windows8+ VM
    if box[:box] !~ /ie6|ie7/i
    config.vm.provision "shell", inline: <<-SHELL
      netsh.exe interface portproxy add v4tov4 3001 10.0.0.3
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
