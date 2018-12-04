required_plugins = %w( vagrant-vbguest  )
required_plugins.each do |plugin|
  unless Vagrant.has_plugin? plugin
    system "vagrant plugin install #{plugin}"
    exit(1)
  end
end

Vagrant.configure("2") do |config|
  config.vm.box = "centos/7"
  config.vm.provision "shell", path: "bootstrap.sh"

  ssh_pub_key = File.readlines("#{Dir.home}/.ssh/id_rsa.pub").first.strip
  config.vm.provision 'shell', inline: "echo #{ssh_pub_key} >> /home/vagrant/.ssh/authorized_keys", privileged: false

  config.vm.define :k8s_node01 do |k8s_node01_config|
    k8s_node01_config.vm.network "private_network", ip: "192.168.5.10"
    k8s_node01_config.vm.host_name = "k8s-node01.local"
    k8s_node01_config.vm.provider :virtualbox do |vb1|
      vb1.customize ["modifyvm", :id, "--memory", "2560"]
      vb1.customize ["modifyvm", :id, "--cpus", "2"]
    end
    if Vagrant.has_plugin?("vagrant-vbguest")
        k8s_node01_config.vbguest.auto_update = true
    end
  end

  config.vm.define :k8s_node02 do |k8s_node02_config|
    k8s_node02_config.vm.network "private_network", ip: "192.168.5.11"
    k8s_node02_config.vm.hostname = "k8s-node02.local"
    k8s_node02_config.vm.provider :virtualbox do |vb2|
      vb2.customize ["modifyvm", :id, "--memory", "2560"]
      vb2.customize ["modifyvm", :id, "--cpus", "2"]
    end
    if Vagrant.has_plugin?("vagrant-vbguest")
      k8s_node02_config.vbguest.auto_update = true
    end

  end

  config.vm.define :k8s_node03 do |k8s_node03_config|
    k8s_node03_config.vm.network "private_network", ip: "192.168.5.12"
    k8s_node03_config.vm.hostname = "k8s-node03.local"
    k8s_node03_config.vm.provider :virtualbox do |vb3|
      vb3.customize ["modifyvm", :id, "--memory", "2560"]
      vb3.customize ["modifyvm", :id, "--cpus", "2"]
    end
    if Vagrant.has_plugin?("vagrant-vbguest")
      k8s_node03_config.vbguest.auto_update = true
    end
  end

end