ENV['VAGRANT_NO_PARALLEL'] = 'yes'

Vagrant.configure("2") do |config|
  config.vm.define "test" do |test_postfix|
    test_postfix.vm.box = "generic/ubuntu2204"
    test_postfix.vm.hostname = "test-gitlab"
    test_postfix.vm.network "private_network", type: "dhcp"
    test_postfix.vm.network "forwarded_port", guest: 8888, host: 8888

    test_postfix.vm.provider :libvirt do |libvirt|
      libvirt.cpus = 2
      libvirt.memory = 2048
      libvirt.driver = "kvm"
    end

    test_postfix.vm.provision "ansible" do |ansible|
      ansible.playbook = "tests/test.yml"
      #ansible.verbose = "vvvv"
      ansible.compatibility_mode = "2.0"
    end
  end 
end
