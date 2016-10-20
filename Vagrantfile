# -*- mode: ruby -*-
# vi: set ft=ruby :

hosts = [
   {name: "server01", ip_address: "192.168.100.101"},
   {name: "server02", ip_address: "192.168.100.102"},
   {name: "server03", ip_address: "192.168.100.103"},
   {name: "server04", ip_address: "192.168.100.104"},
   {name: "server05", ip_address: "192.168.100.105"}
]

Vagrant.configure("2") do |config|
   config.ssh.insert_key = false
   config.vm.box = "minimal/trusty64"
   # Enable ssh access
   config.ssh.forward_agent = true

   # Disable automatic box update checking. If you disable this, then
   # boxes will only be checked for updates when the user runs
   # `vagrant box outdated`. This is not recommended.
   config.vm.box_check_update = false

   poor_mans_dns = ""
   hosts.each do |host|
      poor_mans_dns += host[:ip_address] + "\t" + host[:name] + "\n"
   end

   config.vm.provision :shell, :inline => "
      sed -i \"/$(cat /etc/hostname)/d\" /etc/hosts
      echo 'Adding Vagrant hosts to /etc/hosts:\n" + poor_mans_dns + "'
      echo '\n" + poor_mans_dns + "' >> /etc/hosts
   "

   hosts.each do |host|
      # Blank VM instance
      config.vm.define host[:name] do |box|
         box.vm.hostname = host[:name]
         box.vm.network :private_network, ip: host[:ip_address], nic_type: 'virtio'
         # Create a forwarded port mapping which allows access to a specific port
         # within the machine from a port on the host machine. In the example below,
         # accessing "server01:80" will access port 80 on the guest machine and
         # accessing "server01:81" will access port 81 on the guest machine.
         #box.vm.network "forwarded_port", guest: 80, host: 80 # LB port
         #box.vm.network "forwarded_port", guest: 81, host: 81 # LB admin port

         box.vm.provider "virtualbox" do |vm|
            vm.name = host[:name]
            vm.customize [
               "modifyvm", :id,
               #"--memory", host[:memory],
               "--natdnshostresolver1", "on",
               "--nictype1", "virtio",
               "--usb", "on",
               # Disable USB 2 in order to make it work without Virtualbox Guest Extensions yada blada...
               "--usbehci", "off"
            ]
         end
      end
   end
end
