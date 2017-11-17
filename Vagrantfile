nodes = [
  { :hostname => 'kubernetes-master', :ip => '172.16.66.2', :ram => 4096 },
  { :hostname => 'kubernetes-node1',  :ip => '172.16.66.3', :ram => 2048 },
  { :hostname => 'kubernetes-node2',  :ip => '172.16.66.4', :ram => 2048 },
  { :hostname => 'kubernetes-node3',  :ip => '172.16.66.5', :ram => 2048 }
]

Vagrant.configure("2") do |config|
  if Vagrant.has_plugin?("vagrant-proxyconf")
    config.proxy.http     = "http://xxxxxxxxxxxxxxxxxx"
    config.proxy.https    = "http://xxxxxxxxxxxxxxxxxx"
    config.proxy.no_proxy = "localhost,127.0.0.1,127.0.1.1,.xxx,172.16"
  end

  nodes.each do |node|
    config.vm.define node[:hostname] do |nodeconfig|
      nodeconfig.vm.box = "elastic/ubuntu-16.04-x86_64";
      nodeconfig.vm.hostname = node[:hostname] + ".box"
      nodeconfig.vm.network :private_network, ip: node[:ip]
      memory = node[:ram] ? node[:ram] : 256;
      nodeconfig.vm.provider :libvirt do |domain|
        domain.memory = 4096
        domain.cpus = 2
        domain.nested = true
        domain.volume_cache = 'none'
      end
    end
  end
end
