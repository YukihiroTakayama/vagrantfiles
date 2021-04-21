Vagrant.configure('2') do |config|
  config.vm.box = 'ubuntu/xenial64'

  config.vm.hostname = 'vagranthost'

  config.vm.network :private_network, ip: '192.168.50.10'
  config.vm.network "forwarded_port", guest: 3000, host: 3000
  config.vm.network "forwarded_port", guest: 8080, host: 8080
  config.vm.network "forwarded_port", guest: 80, host: 80

  config.vm.provider :virtualbox do |vb|
    vb.gui = false
    vb.cpus = 4
    vb.memory = 8192
    vb.customize ['modifyvm', :id, '--natdnsproxy1', 'off']
    vb.customize ['modifyvm', :id, '--natdnshostresolver1', 'off']
  end

  config.disksize.size = '30GB'
  config.mutagen.orchestrate = true

  config.vm.synced_folder './', '/home/vagrant/Repositories', type: "rsync",
    rsync_auto: true,
    rsync__exclude: ['node_modules/', 'log/', 'tmp/']

  config.vm.provision :docker, run: 'always'
  config.vm.provision :docker_compose
end
