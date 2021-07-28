Vagrant.configure("2") do |config|
  config.vm.network "public_network"
  config.vm.network "private_network", ip: "192.168.33.11"
  config.vm.synced_folder "/vagrant", "/data"
  config.vm.synced_folder "/vagrant/app", "/app"
  config.vm.boot_timeout = 1440
  config.ssh.username = "vagrant"
  config.ssh.private_key_path = "vagrant.priv"
  config.ssh.forward_agent = true
  config.vm.provider "docker" do |d|
    d.build_dir = "."
    d.has_ssh = true
    d.volumes = ["/home/dev"]
    d.remains_running = false
  end
  config.vm.hostname = "localhost"
  config.vm.network "forwarded_port", guest: 80, host: 7000, host_ip: "127.0.0.1", auto_correct: true
  config.hostmanager.enabled = true
  config.hostmanager.manage_guest = true
  config.vm.provision :hostmanager
  config.vm.provision :ansible do |ansible|
    ansible.playbook = "playbook.yml"
  end
end