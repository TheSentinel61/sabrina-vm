#!/usr/bin/env ruby

Vagrant.configure(2) do |config|
  config.vm.box = 'ubuntu/trusty64'

  config.vm.network :private_network, ip: '10.20.30.40'

  config.vm.provision :file, source: '~/.ssh/id_rsa',     destination: '/home/vagrant/.ssh/id_rsa'
  config.vm.provision :file, source: '~/.ssh/id_rsa.pub', destination: '/home/vagrant/.ssh/id_rsa.pub'

  config.vm.provision :shell, inline: <<-PROVISION
sudo DEBIAN_FRONTEND=noninteractive apt-get -y update && apt-get -y upgrade && apt-get -y install \
git \
vim \
zsh

# Installation of RCM for dotfile management
wget --quiet https://thoughtbot.github.io/rcm/debs/rcm_1.3.0-1_all.deb
checksum=$(sha256sum rcm_1.3.0-1_all.deb | cut -f1 -d' ')
[ "$checksum" = "2e95bbc23da4a0b995ec4757e0920197f4c92357214a65fedaf24274cda6806d" ] && \
sudo dpkg -i rcm_1.3.0-1_all.deb
  PROVISION
end
