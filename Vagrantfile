# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.box = "generic/ubuntu1804"
  config.vm.box_check_update = false
  config.vm.network :forwarded_port, guest: 80, host: 8080
  #config.vm.network "public_network"
  config.vm.provider "virtualbox" do |vb|
    vb.memory = 4096
    vb.cpus = 2
    config.disksize.size = "300GB"
  end

  config.vm.provision "shell", inline: <<-SHELL

    sudo apt install -y gawk wget git diffstat unzip texinfo gcc build-essential chrpath socat cpio python3 python3-pip python3-pexpect xz-utils debianutils iputils-ping python3-git python3-jinja2 libegl1-mesa libsdl1.2-dev pylint3 xterm python3-subunit mesa-common-dev zstd liblz4-tool

  SHELL

  config.vm.provision "shell", privileged: false, inline: <<-SHELL
    # Yocto build
    mkdir ~/yocto
    cd ~/yocto
    git clone git://git.yoctoproject.org/poky
    cd poky
    git checkout -b hardknott

    cd ~/yocto/poky
    source oe-init-build-env build

    # build
    cd ~/yocto/poky/build
    bitbake core-image-weston

  SHELL

end


