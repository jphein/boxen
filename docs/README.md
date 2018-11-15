# BoXenLinux&reg;
An Ubuntu based Linux&reg; distribution for Nonprofits.

It is best described as a collection of open source projects. Configured and extended for Nonprofits. e.g. [Ubuntu], [LTSP], [FreeRDP], and many others! It comes in both server (boxenbrain) and client (boxenbaby) variations. Boxenbrain is all you need if you have a wired network, your clients will boot from the network. However, if you need wireless clients, or remote VPN clients you'll need to use boxenbaby with them. 

BoxenLinux excels at providing thin and zero client driven remote desktop sessions. Linux, Windows, Android and MacOS using ldm, xfreerdp, and xtightvncviwer respectively. It can also provide fatclients for Ubuntu Desktop. [KVM-VDI] provides VDI based remote desktop for all OS's using KVM and Spice. It uses GlusterFS for clustered storage and CTDB for shares. Epoptes provides management and live interaction with all clients.

![alt text](https://jphein.com/wp-content/uploads/2018/11/Screenshot-from-2018-11-11-23-58-02.png)

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

Roadmap: Create live image for both server, and client. Create PXE menu installer for both client and server.

Projects like boXenLinux: www.smartos.org, www.foss-cloud.org/, www.freenas.org, www.edubuntu.org, www.openmediavault.org/, www.nas4free.org/, www.openfiler.org

Installation:
To install, follow this [guide]
Then initiate the below commands in a terminal to copy the config files from this repository:
```sh
cd /
sudo apt install git
sudo git init
sudo git remote add origin https://github.com/jphein/boxen
sudo pull origin master
sudo chmod +x /usr/share/ltsp/screen.d/*
sudo ltsp-update-image -c /
```

To install on the second server or for a headless install: 
PXE boot using existing boXen or LTSP server: 

Add to MAC of second server your existing dhcp conf to tell it to run the installer by default when it PXE boots
```sh
[<mac address>]
 filename /ubuntu-installer/amd64/pxelinux.0
```
Log in remotely into second server, after install
```sh
ssh ubuntu@<ip from dhcp syslog> -p ubuntu 
```
Then run the above steps as if you were installing with CD

List of packages
git byobu ltsp-server-standalone virt-manager epoptes glusterfs-server ctdb

GlusterFS Cluster Filesystem
```sh
sudo gluster peer probe boxen2
sudo gluster volume create vms replica 2 transport tcp boxen1:/vms boxen2:/vms force
sudo gluster volume create vms replica 2 transport tcp boxen1:/storage boxen2:/storage force
mkdir /mnt/vms-pool /mnt/storage-pool
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
