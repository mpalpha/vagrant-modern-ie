## vagrant-modern-ie
Based on the virtual machine images released with the [Modern.IE project](http://dev.modern.ie/), vagrant-modern-ie makes testing IE easier with help from [Vagrant](http://vagrantup.com). The machine images in vagrant-modern-ie are based on the original Modern.IE project images.

## Prerequisites

vagrant-modern-ie requires [Oracle Virtualbox](https://www.virtualbox.org/) and [Vagrant](http://vagrantup.com) be installed and in your path.

## Installation

```bash
git clone https://github.com/mpalpha/vagrant-modern-ie.git
```

## Usage

To list the available virtual machines

```bash
vagrant status
```

To start a new virtual machine.

```bash
vagrant up IE10-Win7
```
  
To remove all virtual machines (**will reset trial**).

```bash
vagrant destroy
```

To remove a specific virtual machine (**will reset trial**).

```bash
vagrant destroy IE10-Win7
```

To start multiple virtual machines at once.

```bash
vagrant up edge-Win10 IE11-Win7 IE10-Win7 IE9-Win7 IE8-Win7
```


## Tips

Redirect 127.0.0.1 to the host ip while in the Windows 8+ VM command prompt.
```bash
netsh interface portproxy add v4tov4 8000 10.0.0.3
```

## Available Vagrant Boxes

ModernIE VMs

* edge-Win10
* IE11-Win7
* IE11-Win8.1
* IE10-Win7
* IE10-Win8
* IE9-Win7
* IE8-Win7
* IE7-Vista  

System Account Credentials

* Username: IEUser  
* Password: Passw0rd!  
