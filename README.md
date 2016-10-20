# Ansible: From Zero to Hero


## What is Ansible
"Ansible is a radically *simple* IT automation engine that automates cloud provisioning, configuration management, application deployment, intra-service orchestration, and many other IT needs." (https://www.ansible.com/how-ansible-works)

In the "good-old-days" you may have applied configuration management changes manually to your environments, but following the "DevOps" movement you have (I hope!) automated these mundane, repetitive tasks using some kind of scripting.

While there is nothing absolutely WRONG with a clean, simple Bash-script to re-configure your application server configuration it is nothing I can recommend because:

1. It is hard to learn, understand and easy to get wrong
1. it is not declarative, i.e. any procedural step that does not work (due to environment variability) can and probably will break the whole script
1. it is not idempotent (you can make it so but this is hard)
1. it does not provide good abstractions which means you have to re-invent them (and get them right)
1. it does not have many pre-built, standardized modules that takes care of well-defined tasks for you

Ansible does this, and more!


## When Ansible
* Do you have the ability to SSH to your infrastructure?
* Do you work in an environment where infrastructure automation is non-existing (i.e. do you SSH to servers and apply manual changes)?
* Do you work in an environment where infrastructure is controlled by someone else than your team?
* Do you work in an environment where infrastructure might be managed by Chef or Puppet in the (distant) future and you can't wait?
* Do you like Guerilla tacticts?

If so, Ansible is for you!

The exercises in this lab are meant as a first step in your journey towards better automation and configuration management!

## Prerequisites
http://xkcd.com/1654/
###1. Lab Environment
This repository contains an simulated environment consisting of 5 hosts. The hosts are small Ubuntu (`minimal/trusty64`) virtual machines, in this case running in VirtualBox. 

In order to run these exercises you first need to install

* Vagrant (manages your virtual machines), which requires a provider like
* VirtualBox (runs your virtual machines), which you configure with

Assuming you have a Mac and none of the above, I recommend the following installation procedure:

1. Install Homebrew: `$ /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"`
1. Install VirtualBox: `$ brew cask install virtualbox`
1. Install Vagrant: `$ brew cask install vagrant`
1. Optional: Install Vagrant Manager: `$ brew cask install vagrant-manager`

In order to start the lab environment, simply run: `$ vagrant up`

This step might take a while but it will start multiple hosts that simulates a (small) server farm.

Lab Environment done!

###2. Control machine
This is the machine that is controlling all other machines (i.e. your laptop). It required the following software:
* Ansible 1.9.6 (provisions your machines with configuration & software), which requires
* Python & SSH: `$ python --version` should output something like `Python 2.7.10`

To install Ansible, perform the following
1. If you don't have pip (Python install packet manager) already: `$ brew install pip`
1. Install Ansible 1.9.6 (yes, there are newer versions): `$ sudo pip install ansible==1.9.6`

Verify that your control machine can run Ansible and use the Lab Environment by running your first Ansible ad-hoc command: `$ ansible all -m ping`

Control machine done; Time for a beer!

## Links
* http://brew.sh/
* https://www.virtualbox.org/wiki/Downloads
* https://www.vagrantup.com/downloads.html
* http://docs.ansible.com/ansible/index.html
   * http://docs.ansible.com/ansible/intro_installation.html
   * http://docs.ansible.com/ansible/intro_installation.html#latest-releases-via-pip
   * http://docs.ansible.com/ansible/ping_module.html
   * http://docs.ansible.com/ansible/playbooks_checkmode.html
* https://github.com/jlund/streisand