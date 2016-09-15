# arch-live
How to make Arch Live-CD
Arch Custom Spin

YouTube Video: https://youtu.be/DqV1BJtJXEA

check list
- at least 10GB of free space
- Arch Linux 64 only
- clear pacman cache; sudo pacman -Scc
- configure everything as root (sudo is fine)
- disable auto update if possible

sudo pacman -S archiso

as root (or sudo)
edit /usr/bin/mkarchiso and add -i to both pacstrap lines
sudo mkdir livecd
sudo cp -r /usr/share/archiso/configs/releng/* /home/midfingr/livecd/
cd livecd
edit build.sh and remove i686 (if 64 bit only)
edit packages.both # add/remove packages

other files to edit:
pacman.conf # add multilib
customize_airootfs.sh # add user, permissions, change usermod
autologin.conf # change to user as per customize_airootfs.sh

- change to: usermod -s /usr/bin/bash root
- example user:

useradd -m -p "" -g users -G "adm,audio,floppy,log,network,rfkill,scanner,storage,optical,power,wheel" -s /bin/bash liveuser
#chmod 700 /root
chown -R liveuser:users /home/liveuser

custom desktop
sudo mkdir /home/midfingr/livecd/airootfs/etc/skel
add .config & .local folders include: .bashrc .xinitrc .xsession .bash_profile

dconf settings

sudo mkdir -p airootfs/usr/bin
sudo cp dump.donf airootfs/usr/bin
sudo leafpad airootfs/usr/bin/spicetheme
sudo mkdir airootfs/etc/skel/.config/autostart
sudo leafpad airootfs/etc/skel/.config/autostart/spicetheme.desktop
