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
This has been furthered by my BoXen Linux project to include:
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
* Download Ubuntu Desktop 18.04.1 ISO here: [Ubuntu] 
* Install Ubuntu 18.04.1 Desktop Minimal Install.
* Run the install script [install]

Manaul install guide here:[guide]

Incomplete List of projects utilized in BoXenLinux: Ubuntu, LTSP, KVM, FreeRDP, KVM-VDI, OpenVPN, and so many more!  

Packages: ssh virt-manager ltsp-server-standalone ltsp-client epoptes dnsmasq xfreerdp grub-ipxe x2goserver git byobu glusterfs-server ctdb apt-cacher

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

To install on the second server or for a headless install, PXE boot using existing boXen or LTSP server: 

```sh
#Add to MAC of second server your existing dhcp conf to tell it to run the installer by default when it PXE boots
[<mac address>]
 filename /ubuntu-installer/amd64/pxelinux.0

#Log in remotely into second server, after install
ssh ubuntu@<ip from dhcp syslog> -p ubuntu 
```
Then run the above steps as if you were installing with CD

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
