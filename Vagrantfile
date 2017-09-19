require 'yaml'
settings = YAML.load_file 'pod.yaml'
Vagrant.configure(2) do |config|
  config.vm.define "router" do |router|
    router.vm.box = "iosxrv"
    router.vm.network :private_network, ip: settings['router']['gig-eth-0'], auto_config: false
    router.vm.network :forwarded_port, guest: 22, host: settings['router']['router_ssh'], host_ip: "0.0.0.0", id: "ssh", auto_correct: true
    router.vm.network :forwarded_port, guest: 830, host: settings['router']['netconf_tcp'], host_ip: "0.0.0.0", auto_correct: false
    router.vm.provision "file", source: "configs/rtr_config", destination: "/home/vagrant/rtr_config"  
    router.vm.provision "shell" do |s|
        s.path =  "scripts/apply_config.sh"
        s.args = ["/home/vagrant/rtr_config"]
  end
end
end
