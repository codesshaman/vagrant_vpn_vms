# Vagrant virual machine with clean centos-7

Your need install vagrant and virtualbox for up this configuration.

Your need install [vagrant](https://github.com/hashicorp/vagrant-installers/releases/tag/v2.3.4.dev%2Bmain "vagrant") and  [virtualbox](https://www.virtualbox.org/ "virtualbox") for up this configuration. Optional you can use [make](https://www.gnu.org/software/make/ "make").

### Step 1

Download box jdesiebenthal/win7 for virtualbox from [vagrantup](https://app.vagrantup.com/jdesiebenthal/boxes/win7 "vagrantup").

Download box bento/centos-7 for virtualbox from [vagrantup](https://app.vagrantup.com/bento/boxes/centos-7 "vagrantup").

### Step 2

Clonr this repository: git clone https://github.com/codesshaman/vagrant_vpn_vms.git

### Step 3

Copy boxes and go inside the repository folder:

``cp ~/Downloads/891fb4c8-4c4b-4f71-b4bd-dc314bbae13f path_to/vagrant_vpn_vms/windows``

``cp ~/Downloads/41bd180b-c435-464a-9100-c3b9220fb263 path_to/vagrant_vpn_vms/centos``

``cd vagrant_vpn_vms``

### Step 4

Inicialize configuration:

``vagrant box add jdesiebenthal/win7 windows``

``vagrant box add bento/centos-7 centos``

or with make:

``make build``

### Step 5

Install configuration:

``vagrant up --provider=virtualbox``

or with make:

``make``

### Step 6

Connect:

``ssh vagrant@192.168.58.48``

or with make:

``make connect``
