Vagrant.configure("2") do |config|
  # 控制节点配置
  config.vm.define "ansible-control" do |control|
    control.vm.box = "generic/ubuntu2204"
    control.vm.network "public_network", bridge: "WLAN"  # 修改为你的物理网卡名称
    control.vm.hostname = "ansible-control"
    control.vm.provider "virtualbox" do |vb|
      vb.memory = "1024"
      vb.cpus = 1
    end
    control.vm.provision "shell", inline: <<-SHELL
      apt-get update
      apt-get install -y ansible openssh-server sshpass
      systemctl enable ssh
      systemctl restart ssh
    SHELL
  end

  # Web节点1配置
  config.vm.define "web-node1" do |web1|
    web1.vm.box = "generic/ubuntu2204"
    web1.vm.network "public_network", bridge: "WLAN"  # 修改为你的物理网卡名称
    web1.vm.hostname = "web-node1"
    web1.vm.provider "virtualbox" do |vb|
      vb.memory = "1024"
      vb.cpus = 1
    end
    web1.vm.provision "shell", inline: <<-SHELL
      apt-get update
      apt-get install -y openssh-server
      systemctl enable ssh
      systemctl restart ssh
    SHELL
  end

  # DB节点配置
  config.vm.define "db-node" do |db|
    db.vm.box = "generic/ubuntu2204"
    db.vm.network "public_network", bridge: "WLAN"  # 修改为你的物理网卡名称
    db.vm.hostname = "db-node"
    db.vm.provider "virtualbox" do |vb|
      vb.memory = "2048"
      vb.cpus = 1
    end
    db.vm.provision "shell", inline: <<-SHELL
      apt-get update
      apt-get install -y openssh-server
      systemctl enable ssh
      systemctl restart ssh
    SHELL
  end
end
