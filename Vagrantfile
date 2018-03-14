Vagrant.configure(2) do |config|

  # haproxy1
  config.vm.define "haproxy1" do |haproxy1|
    haproxy1.vm.box = "ubuntu/xenial64"
    haproxy1.vm.network "private_network", virtualbox__intnet: "10.0.0.0/24", auto_config: false
    haproxy1.vm.network "private_network", virtualbox__intnet: "10.1.0.0/24", auto_config: false
    haproxy1.vm.provision "shell", inline: <<-SHELL
     sudo ifconfig enp0s8 10.0.0.1/24
     apt-get update
     apt-get install git vim -y
    SHELL
  end
  
  # ANSIBLE ##########
  config.vm.define "ansible" do |ansible|
    ansible.vm.box = "trombik/ansible-ubuntu-16.04-amd64"
    ansible.vm.network "private_network", virtualbox__intnet: "mgmt", auto_config: false
    ansible.vm.provision "shell", inline: <<-SHELL
     sudo ifconfig eth1 10.0.0.20/24
     apt-get update
     apt-get install git vim -y
     git clone https://github.qualcomm.com/mattt/ansible-haproxy-keepalived
    SHELL
  end
 
end
