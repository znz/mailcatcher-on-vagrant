# -*- mode: ruby -*-
# vi: set ft=ruby :

BOX_NAME = ENV['BOX_NAME'] || 'trusty'
BOX_URI = ENV['BOX_URI'] || 'https://cloud-images.ubuntu.com/vagrant/trusty/current/trusty-server-cloudimg-amd64-vagrant-disk1.box'

# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = '2'

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.hostname = 'mailcatcher'
  config.vm.box = BOX_NAME
  config.vm.box_url = BOX_URI
  config.vm.network :forwarded_port, guest: 1025, host: 1025
  config.vm.network :forwarded_port, guest: 1080, host: 1080

  config.vm.provider :virtualbox do |vb|
    # Don't boot with headless mode
    vb.gui = true if ENV['VM_GUI']

    #vb.customize ['modifyvm', :id, '--memory', BOX_MEMORY]
  end

  config.vm.provision 'ansible' do |ansible|
    ansible.playbook = 'provision/site.yml'
    ansible.verbose = ENV['ANSIBLE_VERBOSE'] if ENV['ANSIBLE_VERBOSE']
    ansible.tags = ENV['ANSIBLE_TAGS'] if ENV['ANSIBLE_TAGS']
  end
end
