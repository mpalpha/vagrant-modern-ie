##vagrant-modern-ie
Based on the virtual machine images released with the [Modern.IE project](http://dev.modern.ie/), modern-ie-vagrant makes testing IE easier with help from [Vagrant](http://vagrantup.com). The machine images in modern-ie-vagrant are based on the original images with the addition of activating WinRM to make them compatible with the [Vagrant WinRM communicator](http://docs.vagrantup.com/v2/vagrantfile/winrm_settings.html).

##Prerequisites

modern-ie-vagrant requires [Oracle Virtualbox](https://www.virtualbox.org/) and [Vagrant](http://vagrantup.com) be installed and in your path.

##Usage

To list the available virtual machines

```bash
vagrant status
```

To start a new virtual machine

```bash
vagrant up IE10-Win7
```

To start multiple virtual machines at once

```bash
vagrant up edge-Win10 IE11-Win7 IE10-Win7 IE9-Win7 IE8-Win7
```

##Available Vagrant Boxes

ModernIE VMs  
* edge-Win10
* IE11-Win7
* IE11-Win8.1
* IE10-Win7
* IE10-Win8
* IE9-Win7
* IE8-Win7
* IE7-Vista  

System Account Credentials:  
Username: IEUser  
Password: Passw0rd!  

