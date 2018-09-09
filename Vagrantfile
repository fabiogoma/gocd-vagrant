hosts = ['app1', 'app2', 'nginx', 'gocd']

Vagrant.configure('2') do |config|
  config.vm.box = 'centos/7'

  config.vm.synced_folder '.', '/vagrant', disabled: true

  config.vm.provider :libvirt do |libvirt|
    libvirt.driver = 'kvm'
    libvirt.cpus = 2
    libvirt.memory = '4096'
  end

  hosts.each do |hostname|
    config.vm.define hostname do |node|
      node.vm.provision 'ansible' do |ansible|
        ansible.limit = hostname
        ansible.compatibility_mode = '2.0'
        ansible.verbose = false
        ansible.playbook = 'provisioning/playbooks/main.yml'
        ansible.vault_password_file = 'provisioning/playbooks/.vault'
      end
    end
  end
end
