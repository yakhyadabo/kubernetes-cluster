# -*- mode: ruby -*-
# vi: set ft=ruby :

require_relative './vagrant/key_authorization'

Vagrant.configure(2) do |config|

  config.vm.box = "centos/7"
 
  config.ssh.insert_key = false 
  # config.hostmanager.enabled = true
  # config.hostmanager.manage_host = true
  # config.hostmanager.ignore_private_ip = false
  # config.hostmanager.include_offline = true

  authorize_key_for_root config, '~/.ssh/id_rsa.pub'

  # Copy SSH public key
  # config.vm.provision "file", source: "~/.ssh/id_rsa.pub", destination: "/root/.ssh/authorized_keys"
  # config.vm.provision "file", source: "~/.ssh/id_rsa.pub", destination: "/home/vagrant/.ssh/authorized_keys"

  # 192.168.1.1  : The ip that refers to localhost
  # The 'ip route show' command can also be used to display the Ip to use (Ex 10.0.2.15)
  
  [ 
    {:name => 'master', :ip  => '192.168.1.110'},
    {:name => 'minion1',  :ip  => '192.168.1.111'},
    {:name => 'minion2',  :ip  => '192.168.1.112'},
    {:name => 'minion3',  :ip  => '192.168.1.113'}
  ].each do |infos|

    config.vm.define infos[:name] do |host|
      host.vm.network "private_network", ip: infos[:ip]
      # host.vm.network "forwarded_port", guest: 8083, host: infos[:port0]
      # host.vm.network "forwarded_port", guest: 9092, host: infos[:port1]
      host.vm.hostname = "#{infos[:name]}.app.dev"
     # if infos[:name] == "ci"
     #   host.vm.network "forwarded_port", guest: 5000, host: 5000
     # end 
    end
  end

end
