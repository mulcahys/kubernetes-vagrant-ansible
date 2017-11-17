nodes = [
  { :hostname => 'master', :ip => '172.16.66.2', :ram => 4096 },
  { :hostname => 'worker1',  :ip => '172.16.66.3', :ram => 2048 },
  { :hostname => 'worker2',  :ip => '172.16.66.4', :ram => 2048 },
  { :hostname => 'worker3',  :ip => '172.16.66.5', :ram => 2048 }
]

Vagrant.configure("2") do |config|
  nodes.each do |node|
    config.vm.define node[:hostname] do |nodeconfig|
      nodeconfig.vm.box = "elastic/ubuntu-16.04-x86_64";
      nodeconfig.vm.hostname = node[:hostname] + ".box"
      nodeconfig.vm.network :private_network, ip: node[:ip]
      nodeconfig.vm.provider :libvirt do |domain|
        domain.memory = node[:ram] ? node[:ram] : 1024;
        domain.cpus = 2
        domain.nested = true
        domain.volume_cache = 'none'
      end
    end
  end

  if Vagrant.has_plugin?("vagrant-proxyconf")
    config.proxy.http     = ENV['http_proxy']
    config.proxy.https    = ENV['https_proxy']
    addresses = []
    addresses << ENV['no_proxy']
    nodes.each do |node|
      addresses << node[:ip]
    end
    config.proxy.no_proxy = addresses * ","
  end

end
