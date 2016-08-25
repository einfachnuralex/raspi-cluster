# -*- mode: ruby -*-
# # vi: set ft=ruby :

##
# http://blog.scottlowe.org/2014/10/22/multi-machine-vagrant-with-yaml/

# Specify minimum Vagrant version and Vagrant API version
Vagrant.require_version ">= 1.6.0"
VAGRANTFILE_API_VERSION = "2"

# Require YAML module
require 'yaml'

# Read YAML file with box details
servers = YAML.load_file('servers.yaml')

# Create boxes
Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.usable_port_range = 2800..2900
  # Iterate through entries in YAML file
  servers.each do |servers|
    config.vm.define servers["name"] do |srv|
      srv.vm.box = servers["box"]
      srv.vm.hostname = servers["hostname"]
      srv.vm.network "private_network", ip: servers["ip1"], virtualbox__intnet: "cluster"
      srv.vm.provider :virtualbox do |vb|
        vb.name = servers["name"]
        vb.memory = servers["ram"]
        vb.cpus = servers["cpu"]
      end
    end
  end
end
