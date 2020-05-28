BOX_IMAGE = "centos/7"
NODE_COUNT = 1

Vagrant.configure("2") do |config|

  config.vm.provider "virtualbox" do |v|
    v.memory = 1024
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
end