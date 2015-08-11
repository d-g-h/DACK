# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.box = "cloudtrusty64"
  config.vm.box_url = "http://cloud-images.ubuntu.com/vagrant/trusty/current/trusty-server-cloudimg-amd64-vagrant-disk1.box"
  config.vm.provider :virtualbox do |vb|
    vb.customize ["modifyvm", :id, "--memory", "1024"]
    vb.customize ["modifyvm", :id, "--cpus", 2]
    vb.customize ["modifyvm", :id, "--ioapic", "on"]
    #Fix for slow external network connections
    vb.customize ['modifyvm', :id, '--natdnshostresolver1', 'on']
    vb.customize ['modifyvm', :id, '--natdnsproxy1', 'on']
  end
  config.vm.network :private_network, ip: "192.168.50.254"
  config.vm.network :forwarded_port, guest: 80, host: 8080, auto_correct: true
  config.vm.network :forwarded_port, guest: 8000, host: 8000, auto_correct: true
  config.vm.network :forwarded_port, guest: 3306, host: 3306, auto_correct: true
  config.vm.network :forwarded_port, guest: 22, host: 2254, auto_correct: false, id: "ssh"
  # Synced folder
  config.vm.synced_folder ".", "/var/www", :mount_options=> ["dmode=755","fmode=664"], :owner => "www-data", :group => "www-data"
  config.vm.provision :ansible do |ansible|
    ansible.playbook = "dev-nginx.yml"
    ansible.sudo = true
    #For debugging, verbose mode
    #ansible.raw_arguments = ['-vvvv']
  end
  config.vm.define :dack do |dack|
    dack.vm.hostname = "dack"
  end
end
