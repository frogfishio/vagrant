# Vagrant

This is a helper Vagrant configuration for building Nodejs application.

The intent of this file is to standardise on one set of tools, applications 
and versions across development computers to avoid "it worlks on my computer" situations.

## Prerequisites
You will need
* Vagrant https://www.vagrantup.com/downloads.html
* Virtual box https://www.virtualbox.org/wiki/Downloads

You may need git to clone this repo or just download zip

Please note: Sometimes vagrant version requirers an older version of Virtual Box 
(which is exactly the kind of situation we are trying to avoid with this vagrant setup)

## Getting started
Here is how to setup your dev environment

1. Install vagrant and virtual box
2. Download and unpack this repository in a location of your choice
3. Go into the folder with Vagrantfile and type "vagrant up" - this will install your dev environment

After vagrant finished provisionining you can log into the machine by typing "vagrant ssh"

Alternatively you can ssh into the running vagrant machine with: ssh -i ~/.vagrant.d/insecure_private_key vagrant@localhost -p 2222

## Setting up your IDE

1. Download and install Visual Studio Code from https://code.visualstudio.com/
2. Start it and install "Remote SSH" extension
3. Click on a little green box in lower-left corner of editor whhich will popup a menu
4. Choose Remote-SSH -> Open Configuration File ...\\.ssh\config
5. This will open your ssh configuration file, edit it to contain the following configuration

Host localhost
  HostName localhost
  User vagrant
  Port 2222
  IdentityFile ~/.vagrant.d/insecure_private_key

6. After saving it, click on the green box again and choose Remote-SSH Connect to Host
7. Choose localhost

This will connect to running virtual machine and install code server. Once that's done 
you'll be able to edit files remotely as well as when opening terminal it will
automatically open it in a remote machine.

