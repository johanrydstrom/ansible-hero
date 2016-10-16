# Ansible: From Zero to Hero


## What is Ansible
"Ansible is a radically *simple* IT automation engine that automates cloud provisioning, configuration management, application deployment, intra-service orchestration, and many other IT needs." (https://www.ansible.com/how-ansible-works)

In the "good-old-days" you may have applied configuration management changes to your environments, but with the "DevOps" movement you may (I hope) have automated these mundane, repetative tasks using som kind of scripting.

While there is nothing absolutely WRONG with a clean, simple Bash-script to re-configure your application server configuration it is nothing I can recommend because:
1. it is not declarative, i.e. it is up to you to make the script idempotent (which is easy to get wrong)
1. it does not provide good abstractions which means you have to invent them (ok, sometimes this is good thing!)
1. it does not have a lot of standardized modules that take care of well-defined tasks

In my mind, Ansible hits the sweet-spot by providing the right abstraction on scripting. The exercises in this lab are meant as a first step in your journey towards better configuration management!


## Why Ansible
* Do you work in an environment where infrastructure is controlled by someone else than your team?
* Do you work in an environment where infrastructure automation is non-existing (i.e. do you SSH to servers and apply manual changes)?
* Do you work in an environment where infrastructure will be managed by Chef or Puppet in the (distand) future?
* Do you like Guerilla tacticts?
* Do you have the ability to SSH to your infrastructure?

If so, Ansible is for you!

## Who uses it
* Videoplaza/Ooyala
* iZettle
* Com Hem
* ...

## Prerequisites
In order to run these exercises you first need to install
1. Vagrant (manages your virtual machines), which requires a provider like
1. VirtualBox (runs your virtual machines), which you configure with
1. Ansible (provisions your machines with configuration & software), which requires
1. Python & SSH

	`$ python --version` should output something like `Python 2.7.10`

Assuming you have a Mac and none of the above, I recommend the following installation procedure:
1. Install Homebrew: `$ /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"`
1. Install pip (Python install packet manager): `$ brew install pip`
1. Install Ansible 1.9.6 (yes, there are newer versions): `$ sudo pip install ansible=1.9.6`
1. Install VirtualBox: `$ brew cask install virtualbox`
1. Install Vagrant: `$ brew cask install vagrant`
1. Optional: Install Vagrant Manager: `$ brew cask install vagrant-manager`

Bingo, all done!

## Lab Environment
This repository contains an simulated environment consisting of 5 hosts which can be configured to do whatever you want. In order to get the exercise environment up and running you need:
1. Start multiple hosts that simulates a (small) server farm: `$ vagrant up`
1. Verify the environment by running your first Ansible command: `$ ansible servers -i webservers -m ping`

Time for a beer!