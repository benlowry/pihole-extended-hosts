# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.box = "minimal/trusty64"
  config.vm.hostname = "pihole"
  config.vm.provider "virtualbox" do |vb|
     vb.name = "pihole"
     vb.customize ["modifyvm", :id, "--cpus", "1"]
     vb.customize ["modifyvm", :id, "--memory", "512"]
     vb.customize ["modifyvm", :id, "--usb", "off"]
     vb.customize ["modifyvm", :id, "--usbehci", "off"]
  end
  config.vm.network "public_network", ip: "192.168.1.5"
  config.vm.provision "shell", inline: $setup
end

$setup = <<SETUP
echo "nameserver 8.8.8.8" >> /etc/resolv.conf
apt-get -y update
apt-get -y install git curl unzip netcat iptables 
apt-get install -y dnsmasq

echo "nameserver 8.8.8.8" >> /etc/resolv.conf
cd /home/vagrant

git clone git://github.com/StevenBlack/hosts host-blocklist
cat /vagrant/host-update.sh > host-update.sh
ln -s /home/vagrant/host-blocklist /etc/host-blocklist

mkdir -p dnsmasq.d
rm -rf /etc/dnsmasq.d
ln -s /home/vagrant/dnsmasq.d /etc/dnsmasq.d
echo "addn-hosts=/etc/custom.hosts/hosts" > dnsmasq.d/02-custom-hosts.conf
echo "addn-hosts=/etc/host-blocklist/hosts" > dnsmasq.d/03-host-blocklist.conf

mkdir -p custom.hosts
ln -s /home/vagrant/custom.hosts /etc/custom.hosts
cat /vagrant/custom.hosts > custom.hosts/hosts

iptables -A INPUT -p tcp --dport 80 -j ACCEPT
iptables -A INPUT -p udp --dport 53 -j ACCEPT
iptables-save

echo "------------------------------------------------------------------"
echo "Setup script finished."
echo "------------------------------------------------------------------"
echo "Pihole is preconfigured with hosts blocklist and custom domains and"
echo "can be installed and setup completed with:"
echo " $ curl -L https://install.pi-hole.net/ | bash"
echo " $ bash host-update.sh # update everything"
echo "------------------------------------------------------------------"
SETUP
