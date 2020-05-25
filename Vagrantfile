
Vagrant.configure("2") do |config|

  if Vagrant.has_plugin?("vagrant-proxyconf")
    config.proxy.no_proxy = "127.0.0.1,localhost"
  end
  
  config.vm.define "devops-box" do |devbox|
      devbox.vm.box = "ubuntu/bionic64"
      devbox.vm.hostname = "proximity"

      # devbox.vm.box_check_update = false
      devbox.vm.network "forwarded_port", guest: 80, host: 80
      devbox.vm.network "forwarded_port", guest: 8080, host: 8080
      devbox.vm.network "forwarded_port", guest: 443, host: 443
      devbox.vm.network "forwarded_port", guest: 53306, host: 53306
      devbox.vm.network "private_network", ip: "192.168.33.11"
      # devbox.vm.network "public_network"
  
      # Provisioning
      devbox.vm.provision "shell", path: "scripts/provision.sh"

      # Windows
      # devbox.vm.synced_folder "C:/Resources", "/home/vagrant/Resources", mount_optinos: ['dmode=777', 'fmode=755']
  
      # Mac
      devbox.vm.synced_folder "/../../Resources", "/home/vagrant/Resources", mount_optinos: ['dmode=775', 'fmode=644']

      devbox.vm.provider "virtualbox" do |vb|
      #   # Display the VirtualBox GUI when booting the machine
      #   vb.gui = true
      #   # Customize the amount of memory on the VM:
        vb.memory = "4096"
        vb.name = "proximity"
        vb.cpus = 2
        vb.customize ['modifyvm', :id, "--ioapic", "on"]
      end
   end
end
