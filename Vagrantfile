# -*- mode: ruby -*-
# vi: set ft=ruby :

# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = "2"

VB_MEMORY=1024 * 3
VB_CPU =3
NUM_INSTANCES=1


Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|


  # Disable automatic box update checking. If you disable this, then
  # boxes will only be checked for updates when the user runs
  # `vagrant box outdated`. This is not recommended.
  config.vm.box_check_update = false

  # Create a forwarded port mapping which allows access to a specific port
  # within the machine from a port on the host machine. In the example below,
  # accessing "localhost:8080" will access port 80 on the guest machine.
  # config.vm.network "forwarded_port", guest: 80, host: 8080



  # Create a private network, which allows host-only access to the machine
  # using a specific IP.

  config.vm.provider :virtualbox do |vb, override|
    # Don't boot with headless mode
    vb.gui = false
    vb.memory = VB_MEMORY
    vb.cpus = VB_CPU
  end

  (1..NUM_INSTANCES).each do |i|
    config.vm.define vm_name = "nuxeo-%02d" % i do |nuxeo|
      nuxeo.vm.box = "ubuntu/trusty64"
      nuxeo.vm.hostname = vm_name
      nuxeo.vm.network "private_network", ip: "192.168.33.#{i+9}"

      if i == NUM_INSTANCES
        nuxeo.vm.provision "ansible" do |ansible|
          ansible.groups = {
            "db" => ["nuxeo-01"],
            "redis" => ["nuxeo-01"],
            "elastic" => ["nuxeo-01"],
            "nuxeo" => ["nuxeo-01","nuxeo-02","nuxeo-03"],
            "vagrant:children" => ["db", "nuxeo","redis","elastic"],
          }
          ansible.verbose = "v"
          ansible.playbook = "ansible/nuxeo.yml"
          ansible.limit = 'all'
        end
      end

    end
  end





end
