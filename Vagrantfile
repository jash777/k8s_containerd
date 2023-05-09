Vagrant.configure("2") do |config|

  config.vm.define "master" do |master|
    master.vm.box = "bento/ubuntu-22.04"
    master.vm.hostname = "master-node"
  
    # Bridge network adapter for master node
    master.vm.network "public_network", bridge: "Intel(R) 82579V Gigabit Network Connection", ip: "192.168.1.35"
 
  
    master.vm.provider "virtualbox" do |vb|
      vb.memory = "1024"
      vb.cpus = "1"
    end
  
    master.vm.provision "shell", inline: <<-SHELL
      sudo apt-get update
      # Additional provisioning commands for the master node
    SHELL
  end

  config.vm.define "worker" do |worker|
    worker.vm.box = "ubuntu/focal64"
    worker.vm.hostname = "worker-node"
  
    # Bridge network adapter for worker node
    worker.vm.network "public_network", bridge: "Intel(R) 82579V Gigabit Network Connection", ip: "192.168.1.36"
  

  
    worker.vm.provider "virtualbox" do |vb|
      vb.memory = "1024"
      vb.cpus = "1"
    end
  
    worker.vm.provision "shell", inline: <<-SHELL
      sudo apt-get update
      # Additional provisioning commands for the worker node
    SHELL
  end

end
