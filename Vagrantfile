# -*- mode: ruby -*-
# vi: set ft=ruby :
Vagrant.configure(2) do |config|
  # The most common configuration options are documented and commented below.
  # For a complete reference, please see the online documentation at
  # https://docs.vagrantup.com.

  config.vm.box = "ubuntu/trusty64"

  # Disable automatic box update checking. If you disable this, then
  # boxes will only be checked for updates when the user runs
  # `vagrant box outdated`. This is not recommended.
  # config.vm.box_check_update = false

  # Create a forwarded port mapping which allows access to a specific port
  # within the machine from a port on the host machine. In the example below,
  # accessing "localhost:8080" will access port 80 on the guest machine.
  config.vm.network "forwarded_port", guest: 80, host: 5080 # graphite-web
  config.vm.network "forwarded_port", guest: 2003, host: 5003, protocol: 'udp' # graphite

  # Create a private network, which allows host-only access to the machine
  # using a specific IP.
  # config.vm.network "private_network", ip: "192.168.33.10"

  # Create a public network, which generally matched to bridged network.
  # Bridged networks make the machine appear as another physical device on
  # your network.
  # config.vm.network "public_network"

  # config.ssh.forward_agent = true

  config.vm.provider "virtualbox" do |vb|
    # Display the VirtualBox GUI when booting the machine
    # vb.gui = true

    # Customize the amount of memory on the VM:
    vb.memory = "1024"
  end

  config.vm.provision "shell", inline: <<-SHELL
    sudo apt-get update
    sudo DEBIAN_FRONTEND=noninteractive apt-get install -yq --force-yes graphite-web graphite-carbon apache2 libapache2-mod-wsgi

    sudo sh -c 'echo "CARBON_CACHE_ENABLED=true" > /etc/default/graphite-carbon'
    sudo sh -c 'echo "[default]\npattern = .*\nretentions = 10s:10m,1m:1h,10m:1d\n\n" > /etc/carbon/storage-schemas.conf'

    sudo a2dissite 000-default
    sudo cp /usr/share/graphite-web/apache2-graphite.conf /etc/apache2/sites-available
    sudo a2ensite apache2-graphite
    sudo service apache2 reload
  SHELL

  # sudo cp /usr/share/doc/graphite-carbon/examples/storage-aggregation.conf.example /etc/carbon/storage-aggregation.conf
end
