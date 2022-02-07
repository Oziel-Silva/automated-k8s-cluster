
# -*- mode: ruby -*-
# vi: set ft=ruby  :

machines = {
  "master"   => {"memory" => "2048", "cpu" => "2", "ip" => "30", "image" => "ubuntu/focal64"},
  "node01" => {"memory" => "2048",  "cpu" => "2", "ip" => "31", "image" => "ubuntu/focal64"},
  "node02" => {"memory" => "2048",  "cpu" => "2", "ip" => "32", "image" => "ubuntu/focal64"},
  "node03" => {"memory" => "2048",  "cpu" => "2", "ip" => "33", "image" => "ubuntu/focal64"},
}

Vagrant.configure("2") do |config|

  machines.each do |name, conf|
    config.vm.define "#{name}" do |machine|
      machine.vm.box = "#{conf["image"]}"
      machine.vm.hostname = "#{name}.ozielsilva.example"
      machine.vm.network "private_network", ip: "10.0.0.#{conf["ip"]}"
      machine.vm.provider "virtualbox" do |vb|
        vb.name = "#{name}"
        vb.memory = conf["memory"]
        vb.cpus = conf["cpu"]
        vb.customize ["modifyvm", :id, "--groups", "/iac"]
      end
    config.vm.provision "shell", inline: <<-EOF
      HOSTS=$(head -n7 /etc/hosts)
      echo -e "$HOSTS" > /etc/hosts
      echo '10.0.0.30 master.ozielsilva.example' >> /etc/hosts
      echo '10.0.0.31 node01.ozielsilva.example' >> /etc/hosts
      echo '10.0.0.32 node02.ozielsilva.example' >> /etc/hosts
      echo '10.0.0.33 node03.ozielsilva.example' >> /etc/hosts
      EOF
    end
  end
end
