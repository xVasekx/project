MACHINES = {
  :websrv => {
        :box_name => "generic/debian12",
        :vm_name => "websrv",
        :net => [
                   {ip: '192.168.57.10', adapter: 8},
                ]
  },
  :masterdb => {
        :box_name => "generic/debian12",
        :vm_name => "masterdb",
        :net => [
                   {ip: '192.168.57.11', adapter: 8},
                ]
  },

  :slavedb => {
        :box_name => "generic/debian12",
        :vm_name => "slavedb",
        :net => [
                   {ip: '192.168.57.12', adapter: 8},
                ]
  },

  :zabbixsrv => {
        :box_name => "generic/debian12",
        :vm_name => "zabbixsrv",
        :net => [
                   {ip: '192.168.57.14', adapter: 8},
                ]
  },

  :logsrv => {
        :box_name => "generic/debian12",
        :vm_name => "logsrv",
        :net => [
                   {ip: '192.168.57.15', adapter: 8},
            ]
  },
}

Vagrant.configure("2") do |config|

  MACHINES.each do |boxname, boxconfig|
    
    config.vm.define boxname do |box|
   
      box.vm.box = boxconfig[:box_name]
      box.vm.host_name = boxconfig[:vm_name]

      config.vm.provider "virtualbox" do |v|
        v.memory = 1024 
        v.cpus = 1
       end

      if boxconfig[:vm_name] == "logsrv"
       box.vm.provision "ansible" do |ansible|
        ansible.playbook = "ansible/playbook.yml"
        ansible.inventory_path = "ansible/hosts"
        ansible.host_key_checking = "false"
        ansible.become = "true"
        ansible.limit = "all"
       end
      end

      boxconfig[:net].each do |ipconf|
        box.vm.network "private_network", **ipconf
      end

      box.vm.provision "shell", inline: <<-SHELL
        mkdir -p ~root/.ssh
        cp ~vagrant/.ssh/auth* ~root/.ssh
      SHELL
    end
  end
end

