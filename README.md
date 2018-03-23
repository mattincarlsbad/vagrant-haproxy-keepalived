# vagrant-haproxy-keepalived

Get started!
https://www.vagrantup.com/docs/getting-started/

## Network
The Vagrantfile in this repo will build the below network using Ubuntu 16.04 VMs running in Virtualbox.  Try it, it's so easy!
```bash
           +---------+
           | ansible |
           +----+----+
                |.20
   +--+---------+---------+--+ 10.0.0.0/24
      |.1                 |.2
+-----+----+         +----+-----+
| haproxy1 |         | haproxy2 |
+--------+-+         +-+--------+
         |.1           |.2
   +--+--+-------------+--+--+ 10.1.0.0/24
      |.3                 |.4
+-----+----+         +----+-----+
| server1  |         | server2  |
+----------+         +----------+
```
## Installation
1. Install Virtualbox on Windows, Mac, Linux, etc.
   https://www.virtualbox.org/wiki/Downloads
2. Install Vagrant
   https://www.vagrantup.com/downloads.html
3. Install Git (optional) https://git-scm.com/downloads
3. Create a directory for running the vagrant-arista lab:
   ex: U:\vagrant\arista>
4. Copy the "Vagrantfile" contents from this repo to the new directory. 
   Using git: "git clone https://github.qualcomm.com/itnet-dc/vagrant-haproxy-keepalived"
   Or just copy/paste.  Be sure to name the file "Vagrantfile".

## Vagrantup!
1. Start the lab by using the "vagrant up" command in the vagrant-haproxy-keepalived directory:
```bash
[mattt1-mac:~/vagrant/vagrant-ansible-arista] mattt% vagrant up
