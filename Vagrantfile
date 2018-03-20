Vagrant.configure(2) do |config|

  config.vm.define "haproxy1" do |haproxy1|
    haproxy1.vm.box = "ubuntu/xenial64"
    haproxy1.ssh.insert_key = false
    haproxy1.vm.network "private_network", virtualbox__intnet: "10.0.0.0/24", auto_config: false
    haproxy1.vm.network "private_network", virtualbox__intnet: "10.1.0.0/24", auto_config: false
    haproxy1.vm.provision "shell", inline: <<-SHELL
     sudo ifconfig enp0s8 10.0.0.1/24
     sudo ifconfig enp0s9 10.1.0.1/24
     echo 'net.ipv4.ip_forward=1' | sudo tee -a /etc/sysctl.conf
     sudo sysctl -p /etc/sysctl.conf
     apt-get update
     apt-get install git vim python-minimal -y
    SHELL
  end
  
  config.vm.define "haproxy2" do |haproxy2|
    haproxy2.vm.box = "ubuntu/xenial64"
    haproxy2.ssh.insert_key = false
    haproxy2.vm.network "private_network", virtualbox__intnet: "10.0.0.0/24", auto_config: false
    haproxy2.vm.network "private_network", virtualbox__intnet: "10.1.0.0/24", auto_config: false
    haproxy2.vm.provision "shell", inline: <<-SHELL
     sudo ifconfig enp0s8 10.0.0.2/24
     sudo ifconfig enp0s9 10.1.0.2/24
     echo 'net.ipv4.ip_forward=1' | sudo tee -a /etc/sysctl.conf
     sudo sysctl -p /etc/sysctl.conf
     apt-get update
     apt-get install git vim python-minimal -y
    SHELL
  end

  config.vm.define "server1" do |server1|
    server1.vm.box = "ubuntu/xenial64"
    server1.ssh.insert_key = false
    server1.vm.network "private_network", virtualbox__intnet: "10.1.0.0/24", auto_config: false
    server1.vm.provision "shell", inline: <<-SHELL
     sudo ifconfig enp0s8 10.1.0.3/24
     apt-get update
     apt-get install git vim apache2 python-minimal -y
     sudo route add -net 10.0.0.0 netmask 255.255.255.0 gw 10.1.0.1
    SHELL
  end

  config.vm.define "server2" do |server2|
    server2.vm.box = "ubuntu/xenial64"
    server2.ssh.insert_key = false
    server2.vm.network "private_network", virtualbox__intnet: "10.1.0.0/24", auto_config: false
    server2.vm.provision "shell", inline: <<-SHELL
     sudo ifconfig enp0s8 10.1.0.4/24
     apt-get update
     apt-get install git vim apache2 python-minimal -y
     sudo route add -net 10.0.0.0 netmask 255.255.255.0 gw 10.1.0.1
    SHELL
  end

  config.vm.define "ansible" do |ansible|
    ansible.vm.box = "trombik/ansible-ubuntu-16.04-amd64"
    ansible.vm.network "private_network", virtualbox__intnet: "10.0.0.0/24", auto_config: false
    ansible.vm.provision "shell", inline: <<-SHELL
     sudo ifconfig eth1 10.0.0.20/24
     apt-get update
     apt-get install git vim -y
     wget -P .ssh/ "http://kook.qualcomm.com/haproxy/id_rsa"
     chmod 400 .ssh/id_rsa && chown vagrant .ssh/id_rsa
     git clone https://github.qualcomm.com/mattt/ansible-haproxy-keepalived
     sudo route add -net 10.1.0.0 netmask 255.255.255.0 gw 10.0.0.1
    SHELL
  end
 
end
