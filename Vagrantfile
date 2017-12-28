Vagrant.configure("2") do |config|
  config.vbguest.auto_update = false
  config.vm.box = "generic/fedora27"
  config.useradd.users = ['kaushikc']
  config.vm.provision "shell", inline: <<-SHELL
    yum groupinstall -y "Fedora Workstation"
    yum install -y xmonad ghc-xmonad-contrib{,-devel} xmobar
    yum install -y gdm gnome-desktop3 git
    systemctl enable gdm
    systemctl enable gdm.service
    systemctl start gdm
    systemctl start graphical.target
    chown -R vagrant:vagrant /home/vagrant/.xmonad
  SHELL

  config.vm.provision "shell", privileged: false, inline: <<-SHELL
    if [ ! -d /home/vagrant/code/dotfiles ] ; then
      git clone https://github.com/ckaushik/dotfiles /home/vagrant/code/dotfiles
    fi
    mkdir -p /home/vagrant/code
    rm -rf /home/vagrant/.xmonad/xmonad.hs
    ln -s /home/vagrant/code/dotfiles/xmonad/xmonad.hs /home/vagrant/.xmonad/xmonad.hs
  SHELL
end
