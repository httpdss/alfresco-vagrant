# -*- mode: ruby -*-
# vi: set ft=ruby :


Vagrant.configure("2") do |config|
  config.vm.box = "precise64"
  # config.vm.network :forwarded_port, guest: 8080, host: 7070
  config.vm.network :private_network, ip: "192.168.33.14"

  config.vm.provision :shell, :inline => "gem install chef --version '>= 11.0.0' --no-rdoc --no-ri --conservative"

  config.vm.provider :virtualbox do |vb|
    vb.customize ["modifyvm", :id, "--memory", "1500"]
  end

  config.vm.provision :chef_solo do |chef|
    chef.cookbooks_path = "cookbooks"
    # chef.add_recipe "apt"
    chef.add_recipe "build-essential"
    chef.add_recipe "rvm::vagrant"
    chef.add_recipe "rvm::system"
    chef.add_recipe "chef-client"
    chef.add_recipe "git"
    chef.add_recipe "alfresco"
    # chef.add_recipe "collectd::client"
    # chef.add_recipe "collectd_plugins::syslog"
    # chef.add_recipe "collectd_plugins::cpu"
    # chef.add_recipe "collectd_plugins::df"
    # chef.add_recipe "collectd_plugins::disk"
    # chef.add_recipe "collectd_plugins::interface"
    # chef.add_recipe "collectd_plugins::memory"
    # chef.add_recipe "collectd_plugins::swap"

    chef.json = {
        :mysql => {
            :server_root_password => "root",
            :server_repl_password => "root",
            :server_debian_password => "root",
            :bind_address => "127.0.0.1"
        },
        :alfresco => {
          :db => {
            :user => 'root',
            :password => 'root',
            :database => 'alfresco',
          }
        },
        :java => {
          :oracle => {
            "accept_oracle_download_terms" => true
          },
          :install_flavor => "oracle"
        }
    }
  end
end
