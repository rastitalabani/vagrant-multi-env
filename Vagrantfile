BOX_IMAGE = "ubuntu/bionic64"
NODE_COUNT = 0

Vagrant.configure("2") do |config|

  config.vm.provider "virtualbox" do |v|
    v.memory = 2048
    v.cpus = 2
  end

  if Vagrant.has_plugin?("vagrant-proxyconf")
    config.proxy.http     = ENV["http_proxy"]
    config.proxy.https    = ENV["https_proxy"]
    config.proxy.no_proxy = ENV["no_proxy"]
  end

  config.vm.define "master" do |subconfig|
    subconfig.vm.box = BOX_IMAGE
    subconfig.vm.hostname = "master"
    subconfig.vm.network "private_network", :ip => "192.168.56.100", :name => 'vboxnet0', :adapter => 2
  end
  
  (1..NODE_COUNT).each do |i|
    config.vm.define "node#{i}" do |subconfig|
      subconfig.vm.box = BOX_IMAGE
      subconfig.vm.hostname = "node#{i}"
      subconfig.vm.network "private_network", :ip => "192.168.56.10#{i+1}", :name => 'vboxnet0', :adapter => 2
    end
  end


  # ... adding own ssh keys 
  config.vm.provision "file", 
    source: "~/.ssh/id_rsa.pub", 
    destination: "~/.ssh/me.pub"


  config.vm.provision "shell", inline: <<-SHELL
    cat /home/vagrant/.ssh/me.pub >> /home/vagrant/.ssh/authorized_keys
  SHELL


end