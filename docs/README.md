# BoXenLinux&reg;
An Ubuntu based Linux&reg; distribution for Nonprofits.

BoXenLinux is a collection of open source projects. Configured and extended for Nonprofits. It comes in both server (BoXenbrain) and client (BoXenbaby) variations. BoXenLinux excels at providing zero, and thin client driven local or remote desktop sessions. Linux, Windows, MacOS, and more. Using ldm, xfreerdp, and vncviewer respectively. It can also provide fat clients for Ubuntu Desktop. Utilizing [KVM-VDI] allows VDI managedment for all types of virtual Desktops using KVM and Spice. Great for MacOS, Windows 10, Androidx86, ChromiumOS, and Raspbian. A PFsense virtual machine, or OpenVPN is used to secure all wireless and wan connections. It uses GlusterFS for clustered storage and CTDB for shares. Epoptes provides management and live interaction with all clients. 

BoXenbrain is all you need if you have a wired network. All networked clients will boot the client of your choose automatically over the network. However, if you need wireless, or remote VPN clients you'll want to install BoXenbaby to the internal drive or a USB drive of each wireless or wan client. BoXenbaby is simply Ubuntu 18.04.1 Desktop minimal preseeded with openvpn, xfreerdp-nightly, and other modern clients. To install, utilize an existing BoXen network for automatic net boot install. You can also download the USB image, and install manually. 

BoXenbrain is more complex, and is described below.

![alt text](https://jphein.com/wp-content/uploads/2018/11/Screenshot-from-2018-11-11-23-58-02.png)
<img src="https://user-images.githubusercontent.com/19301265/48688498-5d159380-eb7b-11e8-8610-6da0a67a0182.png" width="15%"></img> <img src="https://user-images.githubusercontent.com/19301265/48688511-6999ec00-eb7b-11e8-861a-dcc4e471e8f8.png" width="15%"></img> <img src="https://user-images.githubusercontent.com/19301265/48688519-70c0fa00-eb7b-11e8-977e-1a5fe2970a6a.png" width="15%"></img> <img src="https://user-images.githubusercontent.com/19301265/48688523-74ed1780-eb7b-11e8-968f-967c84126a2e.png" width="15%"></img> <img src="https://user-images.githubusercontent.com/19301265/48688541-7c142580-eb7b-11e8-9fb9-d82e6bcda8cb.png" width="15%"></img> <img src="https://user-images.githubusercontent.com/19301265/48688546-80404300-eb7b-11e8-8245-66d5b864f3ce.png" width="15%"></img> 

Ubuntu and LTSP can provide a platform for providing desktops environments in many different ways.

LTSP already comes with these client scripts:
```sh
kiosk – Firefox running locally on thin client.
ldm – Linux desktop running remotely on local server.
menu – Interactive Menu
shell – Drop to root bash shell running locally on thin client.
ssh – Secure Shell for remote terminal on local or remote server.
telnet – unsecure ssh 😉 running remotely on local or remote server.
xdmcp – Raw Xorg linux desktop running remotely on server.
xfreerdp – RDP for Windows desktop running remotely on local or cloud server.
xterm – xterm terminal running locally on thin client.
```
This has been furthered by the BoXenLinux project to include:
```sh
freerdp-nightly – Nightly builds of xfreerdp to take advantage of Microphone redirection and the latest graphics codecs.
rdpgui – Gui for displaying a welcome website, and to prompt for credentials when using xfreerdp-nightly.
vdi – KVM-VDI LTSP client, see github.com/Seita…
vnc – VNCviewer for remote desktop on local or remote Android or MacOS computers.
spice – virt-viewer for KVM Virtualization software. Can provide remote access to local or remote desktops of ANY kind you can virtualize.
x2go - Linux remote desktop for local or remote servers. 
welcome - Gui Welcome window to display a welcome URL using zenity
```
Most of the configuration is done in the lts.conf file
https://github.com/jphein/boxen/blob/master/var/lib/tftpboot/amd64/lts.conf

Installation:
If you already have a BoXenbrain on your network, simply plug your second in, and boot to the PXE menu where you will be presented with an option to install BoXenbrain. However, if this is your first brain on the network you need to follow the steps below.
* Download Ubuntu Desktop 18.04.1 ISO here: [Ubuntu] 
* Install Ubuntu 18.04.1 Desktop Minimal Install.
* Run the install script [install]

Manual install guide resided here: [guide]

Incomplete List of projects utilized in BoXenLinux: Ubuntu, LTSP, KVM, FreeRDP, KVM-VDI, OpenVPN, and so many more! Thank you!!! 

Packages on top of the Ubuntu 18.04.1 Desktop minimal install: ssh virt-manager ltsp-server-standalone ltsp-client epoptes dnsmasq xfreerdp grub-ipxe x2goserver git byobu glusterfs-server ctdb apt-cacher

Roadmap: 

* Create live image for both server, and client with installer using mkusb. and/or respin, and/or preseed file.
https://askubuntu.com/questions/930233/how-can-i-make-a-bootable-unattended-usb-restore-disk/930489#930489

* Create PXE menu installer for both client and server.
  * Client --> LTSP menu (default)
  * Install boxen baby (wifi or vpn remote) client -- ubuntu bionic desktop minimal install with xfreerdo-ngihtly
  * Install boxen brain server -- preseeded ubuntu with boxen install script
  * Boot first HD
  * netboot.xyz https://netboot.xyz/booting/tftp/
https://wiki.ubuntu.com/UEFI/PXE-netboot-install
https://help.ubuntu.com/community/UbuntuLTSP/LTSPMultiboot

```sh
#ltsp: This is the place for support of LTSP.  Ask your question and hang around for an answer.  Check IRC logs at http://irclogs.ltsp.org
[19:56] == jphein [b8178628@gateway/web/freenode/ip.184.23.134.40] has joined #ltsp
[19:56] -ChanServ- [#ltsp] Welcome to the Linux Terminal Server Project's irc channel
[19:58] <jphein> Hello to everyone. =] I have a nice LTSP install in KVM. It's using Ubuntu 18.04.1, with the chrootless dnsmasq proxy method
[19:59] <jphein> However, when I run ltsp-update-kernels my pxe config doesn't pick up the changes I make in /etc/ltsp/udpate-kernels.conf
[20:00] <jphein> my /var/lib/tftpboot/amd64pxelinux.cfg/ directory remains unchanged
[20:01] <jphein> When I make the changes directly in the files it works well
[20:09] <jphein> Am I missing something?
[21:56] <alkisg> jphein: yes, /usr/share/ltsp/update-kernels
[21:56] <alkisg> This transfers /etc/ltsp/update-kernels.conf to /boot/pxelinux.cfg/default
[21:56] <alkisg> Then ltsp-update-image puts it in /opt/ltsp/images/amd64.img
[21:57] <alkisg> And finally ltsp-update-kernels gets it from amd64.img and puts it to tftp
[21:57] <jphein> Thank you! I'll try it out. =]
[21:57] <alkisg> It's so complicated that I wanted to get rid of it and just use a static file :D
[21:59] <jphein> hahaha
[22:08] <jphein> So it never goes to /var/lib/tftpboot/ltsp/amd64/pxelinux.cfg/ ?
[22:17] <jphein> I'd like to install Ubuntu as a pxe option before my ltsp menu
[22:32] <alkisg> jphein: sure, it goes to pxelinux.cfg after the 4 steps I mentioned above
[22:38] <jphein> lol!
```

```sh
#ltsp: This is the place for support of LTSP.  Ask your question and hang around for an answer.  Check IRC logs at http://irclogs.ltsp.org
[21:36] == jphein [b8178628@gateway/web/freenode/ip.184.23.134.40] has joined #ltsp
[21:36] -ChanServ- [#ltsp] Welcome to the Linux Terminal Server Project's irc channel
[21:37] <jphein> Hello! =] Does anyone know where I would put my install-ubuntu kernels so that update-kernels picks them up and presents them on the PXE menu?
[21:39] <jphein> Or, do I have to edit the pxelinux.cfg/default symlink manually?
[21:39] == vagrantc [~vagrant@unaffiliated/vagrantc] has joined #ltsp
[21:41] <jphein> This is my https://github.com/jphein/boxen/blob/master/etc/ltsp/update-kernels.conf
[21:44] <jphein> I suppose I can edit my dnsmasq.d/ to add the mac address of the client I'd want to install. With the ubuntu-install pxe boot config.
[21:48] <jphein> I'm also having issues with the chrootless method in the Azure cloud. Seems the Azure kernel may not have all the right input drivers for KVM?
[22:25] <alkisg> jphein: I'm not sure what you're asking; why do you need more than one kernel?
[22:25] <alkisg> If you only keep one kernel, then ltsp will pick them up
[22:26] <alkisg> Now if you want multiple kernels, ltsp will pick up the latest
[22:26] <jphein> Sorry, let me rephrase that. Do you know of  a simple way to present the PXE client user with a menu to install Ubuntu?
[22:26] <alkisg> So if e.g. azure has 4.1, and you manually install 4.15, then the server will have 4.1 and the clients 4.15, without involving any configs
[22:26] <jphein> cool
[22:26] <alkisg> jphein: ah sure, you just expose the .iso etc
[22:27] <alkisg> But the "ltsp way to install a client" is to netboot it and cp -a /run/initramfs/rofs /target
[22:27] <alkisg> I.e. to clone the ltsp image...
[22:27] <jphein> that's exactly what i want
[22:28] <alkisg> You can also easily netboot it, and run: kvm -cdrom /path/to/windows -hda /dev/sda, so that you can even install windows while booted as an ltsp client
[22:28] <alkisg> All those don't involve pxelinux at all
[22:28] <alkisg> You do those via epoptes after the client boots normally via ltsp
[22:28] <jphein> oh yes kvm
[22:28] <alkisg> (or locally)
[22:29] <jphein> with epoptes
[22:29] <jphein> nice
[22:29] <alkisg> I usually don't want to leave my chair, so I do all clients via epoptes
[22:29] <jphein> haha =]
[22:29] <alkisg> So I can be installed 3 different OSes on 3 clients without me going there
[22:30] <alkisg> *I can install, meh
[22:30] <alkisg> I can be installing. OK, got it :P
[22:30] <jphein> thank you , again!
[22:30] <alkisg> np
[22:30] <jphein> I like that solution a lot.
[22:31] <jphein> Do you know the simplest way to preseed an Ubuntu installation with a few changes?
[22:32] <jphein> wcp -a /run/initramfs/rofs /target
[22:32] <jphein> Do I make a screen script?
[22:33] <alkisg> jphein: let's clear something up
[22:34] <alkisg> cp is for cloning the ltsp image
[22:34] <alkisg> kvm is for installing ubuntu from an .iso
[22:34] <alkisg> preseeding only applies to the iso
[22:34] <alkisg> So which one are you asking about?
[22:35] <jphein> hahaha, I'm just very curious
[22:35] <jphein> =]
[22:35] <jphein> i like all of them
[22:35] <jphein> but I want to know more about the cp -a
[22:35] <jphein> it's a simple as that?
[22:36] <jphein> cloning
[22:36] <alkisg> I don't make screen scripts for such simple things; I do make scripts that I run either from epoptes or directly from the client
[22:36] <alkisg> cp,  add user, install grub
[22:36] <alkisg> You can also have a vm on the server, and use dd, to avoid all that
[22:36] <jphein> oh i see
[22:37] <jphein> using qcow?
[22:37] <jphein> or raw img
[22:37] <alkisg> E.g. I have bionic-mate in vbox, then i expose it via nbd, and I dd if=/dev/nbd2 of=/dev/sda on the clients, and it's ready
[22:37] <alkisg> Both  can be done, qemu-nbd supports qcow and vdi and vmdk and raw
[22:38] <jphein> so many ways
[22:38] <jphein> that is the one i'll use since I already have the vm
[22:38] <alkisg> You can even login normally as a user on the client, so that your image is accessible by sshfs in /home/username
[22:38] <alkisg> So then you do dd if=/home/username/vms/myvm of=/dev/sda, done
[22:38] <alkisg> No scripts, no screen scripts, nothing
[22:39] <alkisg> You may only need to resize2fs /dev/sda1 afterwards, so that it extends to all the disk size
[22:39] <jphein> right
[22:41] <vagrantc> and you're doing this in a user with sudo privledges or something?
[22:41] <jphein> yes
[22:41] <alkisg> Yup, with LDM_HASH_PASSWORD=True; or via epoptes :)
[23:34] <jphein> Which commands do you run after a cp -a /run/initramfs/rofs /target ? Install grub?
[00:16] <alkisg> jphein: mount /dev/sda1 /mnt; cd /mnt; for d in proc sys dev dev/pts; do mount --bind /$d $d; done; chroot . dpkg-reconfigure grub-pc; umount dev/pts dev sys proc
```

To install on the second server or for a headless install, PXE boot using existing boXen or LTSP server: 

```sh
#Add to MAC of second server your existing dhcp conf to tell it to run the installer by default when it PXE boots
[<mac address>]
 filename /ubuntu-installer/amd64/pxelinux.0

#Log in remotely into second server, after install
ssh ubuntu@<ip from dhcp syslog> -p ubuntu 
```
Then run the above steps as if you were installing with CD

* Create Preseed file for PXE installers.
https://diegolemos.net/2017/08/06/pxe-booting/
https://help.ubuntu.com/lts/installation-guide/example-preseed.txt
https://gist.github.com/skx/ecc3a429eb11a3c7f022
https://help.ubuntu.com/lts/installation-guide/armhf/apbs02.html
https://www.syslinux.org/wiki/index.php?title=PXELINUX

Interesting Projects:

* selivan / thinclient
Tools to build custom Ubuntu image, that boots over network and works entirely from RAM. 

* AdnanHodzic / displaylink-debian
DisplayLink driver installer for Debian/Ubuntu based Linux distributions.

* kenorb-contrib / isorespin
Script to allow Ubuntu ISO to be respun and customized ("remastered") to create a new ISO

* t413 / SMS-Tools
Import / Export / Merge tool for your Android/iOS/GV text message history.

* antonym / netboot.xyz
Network bootable operating system installer based on iPXE
 
* mbusb / multibootusb
Create multiboot live Linux on a USB disk...
 
* freenas / freenas
FreeNAS Git Repository

* Thinstation / thinstation
A framework for making thin and light Linux based images for x86 based machines and thinclients.

* TigerVNC / tigervnc
High performance, multi-platform VNC client and server
 
* xbgmsharp / ipxe-buildweb
iPXE Prebuilt binary web interface

* Seitanas / kvm-vdi

* www.smartos.org
* www.foss-cloud.org/
* www.edubuntu.org
* www.openmediavault.org/
* www.nas4free.org/
* www.openfiler.org

Once can initiate the below commands in a terminal to copy the config files from this repository to keep updated:
Not working
```sh
cd /
sudo apt install git
sudo git init
sudo git remote add origin https://github.com/jphein/boxen
sudo pull origin master
sudo chmod +x /usr/share/ltsp/screen.d/*
sudo ltsp-update-image -c /
```

The registered trademark Linux® is used pursuant to a sublicense from the Linux Foundation, the exclusive licensee of Linus Torvalds, owner of the mark on a world-wide basis.
© 2018 Canonical Ltd. Ubuntu and Canonical are registered trademarks of Canonical Ltd.

[//]: # (These are reference links used in the body of this note and get stripped out when the markdown processor does its job. There is no need to format nicely because it shouldn't be seen. Thanks SO - http://stackoverflow.com/questions/4823468/store-comments-in-markdown-syntax)

[git]: <https://github.com>
[KVM-VDI]: <https://github.com/Seitanas/kvm-vdi>  
[FreeRDP]: <http://www.freerdp.com/>  
[LTSP]: <https://github.com/gentoo-mirror/ltsp>
[jp]: <https://github.com/jphein>
[boxen]: <https://github.com/jphein/boxen>
[Ubuntu]: <http://www.ubuntu.com/download/desktop>
[guide]: <https://jphein.com/how-to-provide-a-windows-desktop-experience/>
[install]: <https://github.com/jphein/boxen/blob/master/boxenbrain>
[dill]: <https://github.com/joemccann/dillinger>
   [git-repo-url]: <https://github.com/joemccann/dillinger.git>
   [john gruber]: <http://daringfireball.net>
   [@thomasfuchs]: <http://twitter.com/thomasfuchs>
   [df1]: <http://daringfireball.net/projects/markdown/>
   [markdown-it]: <https://github.com/markdown-it/markdown-it>
   [Ace Editor]: <http://ace.ajax.org>
   [node.js]: <http://nodejs.org>
   [Twitter Bootstrap]: <http://twitter.github.com/bootstrap/>
   [keymaster.js]: <https://github.com/madrobby/keymaster>
   [jQuery]: <http://jquery.com>
   [@tjholowaychuk]: <http://twitter.com/tjholowaychuk>
   [express]: <http://expressjs.com>
   [AngularJS]: <http://angularjs.org>
   [Gulp]: <http://gulpjs.com>

   [PlDb]: <https://github.com/joemccann/dillinger/tree/master/plugins/dropbox/README.md>
   [PlGh]:  <https://github.com/joemccann/dillinger/tree/master/plugins/github/README.md>
   [PlGd]: <https://github.com/joemccann/dillinger/tree/master/plugins/googledrive/README.md>
   [PlOd]: <https://github.com/joemccann/dillinger/tree/master/plugins/onedrive/README.md>
