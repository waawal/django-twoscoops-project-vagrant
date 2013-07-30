MEMORY = ENV['DJANGO_VAGRANT_MEMORY'] || '512'
CORES = ENV['DJANGO_VAGRANT_CORES'] || '1'


Vagrant.configure("2") do |config|

  config.vm.box = "precise64"
  config.vm.box_url = "http://files.vagrantup.com/precise64.box"
  config.vm.hostname = "django"

  config.vm.provider :vmware_fusion do |v, override|
    override.vm.box = "precise64"
    override.vm.box_url = "http://files.vagrantup.com/precise64_vmware.box"
    v.vmx["memsize"] = MEMORY
    v.vmx["numvcpus"] = CORES
  end

  config.vm.provider :virtualbox do |v, override|
    v.customize ["modifyvm", :id, "--memory", MEMORY.to_i]
    v.customize ["modifyvm", :id, "--cpus", CORES.to_i]
  end

  config.vm.provision :ansible do |ansible|
    ansible.playbook = "provisioning/site.yml"
    ansible.inventory_file = "provisioning/ansible_hosts"
  end

end
