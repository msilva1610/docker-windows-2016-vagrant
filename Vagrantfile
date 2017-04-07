Vagrant.configure("2") do |config|
  config.vm.box = "windows-2016-amd64"
  config.vm.provider "virtualbox" do |vb|
    vb.linked_clone = true
    vb.memory = 4096
    vb.customize ["modifyvm", :id, "--clipboard", "bidirectional"]
    vb.customize ["modifyvm", :id, "--draganddrop", "bidirectional"]
  end
  config.vm.provision "shell", inline: "Uninstall-WindowsFeature Windows-Defender-Features" # because defender slows things down a lot.
  config.vm.provision "reload"
  config.vm.provision "windows-update"
  config.vm.provision "shell", path: "ps.ps1", args: "provision-chocolatey.ps1"
  config.vm.provision "shell", path: "ps.ps1", args: "provision-base.ps1"
  config.vm.provision "reload"
  config.vm.provision "shell", path: "ps.ps1", args: "provision-containers-feature.ps1"
  config.vm.provision "reload"
  config.vm.provision "shell", path: "ps.ps1", args: "provision-docker.ps1"
end