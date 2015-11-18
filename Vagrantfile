# -*- mode: ruby -*-
# vi: set ft=ruby :
Vagrant.configure(2) do |config|

  # Every Vagrant development environment requires a box. You can search for
  # boxes at https://atlas.hashicorp.com/search.
  config.vm.box = 'debian/jessie64'
  config.vm.box_check_update = false

  config.vm.define "db01" do |db01|
      db01.vm.hostname = "db01"
      db01.vm.network 'private_network', type: 'dhcp'
  end
  config.vm.define 'app01' do |app01|
      app01.vm.hostname = 'app01'
      app01.vm.network 'private_network', type: 'dhcp'
  end
  config.vm.define 'app02' do |app02|
      app02.vm.hostname = 'app02'
      app02.vm.network 'private_network', type: 'dhcp'
  end
  config.vm.define "lb01" do |lb01|
      lb01.vm.hostname = "lb01"
      lb01.vm.network 'private_network', type: 'dhcp'
      # We only run the provisioner once, for all boxes at once instead of each
      # box separately to get advantage of ansible's internal fact cache without
      # having to setup fact caching. So only run it for the last VM
      lb01.vm.provision 'ansible' do |ansible|
          ansible.groups = {
              'appservers' => ['app01', 'app02'],
              'adm_runner' => ['app01'],
              'dbservers'  => ['db01'],
              'webservers' => ['lb01'],
          }
          ansible.limit = 'all'
          ansible.playbook = 'servermon.yaml'
      end
  end
end
