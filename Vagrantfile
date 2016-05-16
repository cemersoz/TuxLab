# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure(2) do |vagrant|

  # Provider Setup
    vagrant.vm.provider "virtualbox" do |provider, override|
      vagrant.vm.box = "ubuntu/trusty64"

    end

    vagrant.vm.provider "virtualbox" do |v|
      v.memory = 1024
      v.cpus = 1
    end

  # Meteor Host
    vagrant.vm.define "meteor" do |meteor|
      meteor.vm.network :forwarded_port,
        guest: 80,
        host: 8080,
        auto_correct: false

      meteor.vm.network "private_network", ip: "10.100.199.203"

      meteor.vm.provision :ansible do |ansible|
        ansible.playbook = "./ansible/meteor.yml"
        ansible.groups = {
          "vagrant" => ["meteor"]
        }
      end
    end

  # Docker Host
    vagrant.vm.define "dockerhost" do |dockerhost|

      dockerhost.vm.network "private_network", ip: "10.100.199.201"

    end

  # Docker Swarm Host
    vagrant.vm.define "dockerswarm" do |dockerswarm|

       dockerswarm.vm.network "private_network", ip: "10.100.199.200"
    end

  # MongoDB Host
    vagrant.vm.define "mongodb" do |mongodb|

      mongodb.vm.network "private_network", ip: "10.100.199.202"

      mongodb.vm.provision :ansible do |ansible|
        ansible.playbook = "./ansible/mongodb.yml"
        ansible.groups = {
          "vagrant" => ["mongodb"]
        }
      end

    end

end
