# BoXenLinux &reg;
An Ubuntu based Linux distribution for Nonprofits

![alt text](https://jphein.com/wp-content/uploads/2018/11/Screenshot-from-2018-11-11-23-58-02.png)

```sh
Files contained within this repository:
/var/lib/tftpboot/ltsp/amd64/lts.conf #Menu driven Desktop chooser
/etc/ltsp/ltsp-build-client.conf      #Build your LTSP client image with the greek schools repo, xfreerdp-nightly, and epoptes.
/opt/ltsp/amd64/usr/share/ltsp/screen.d/xfreerdp-nightly #Symlink to xfreerdp if you want to run nightlies.
/opt/ltsp/amd64/usr/share/ltsp/screen.d/rdpgui           #To prompt for creds needs xfreerdp-prompt as well. 
/opt/ltsp/amd64/usr/share/ltsp/screen.d/xfreerdp-prompt  #To prompt for cred using xfreerdp-nightly.
/opt/ltsp/amd64/usr/share/ltsp/screen.d/vdi              #KVM-VDI LTSP client, see https://github.com/Seitanas/kvm-vdi/
/opt/ltsp/amd64/usr/share/ltsp/screen.d/vncviewer        #Vnc
/opt/ltsp/amd64/usr/share/ltsp/screen.d/remote-viewer    #Spice
```
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
```
Open source zeroclient VDI project based on Ubuntu Linux [LTSP] and [KVM-VDI]
[LTSP] provides thinclient driven session based remote desktop for:
Linux, Windows, and MacOS using ldm, xfreerdp, and xtightvncviwer respectively.
It also, provides fatclients for Ubuntu Desktop.
[KVM-VDI] provides VDI based remote desktop for all OS's using KVM and Spice.
It uses GlusterFS for clustered storage and CTDB for shares.
Epoptes provides management and live interaction with all clients.

Roadmap: Have an Ubuntu cloud version for large nonprofits with 6 servers or more. Make into a .deb package. Create LiveCD, and PXE LiveBoot.

Projects like boXenLinux: www.smartos.org, www.foss-cloud.org/, www.freenas.org, www.edubuntu.org, www.openmediavault.org/, www.nas4free.org/, www.openfiler.org

To install, use an [Ubuntu LiveCD for Ubuntu 18.04.01 Desktop][Ubuntu] LiveCD iso. 
Then run the below in a terminal.

```sh
sudo apt-get install git byobu ltsp-server-standalone qemu-kvm libvirt-bin ubuntu-vm-builder bridge-utils virt-manager epoptes glusterfs-server ctdb#To install packages.
#sudo adduser `id -un` libvirtd
sudo gpasswd `id -un` epoptes
#To have your own configs installed. Fork jphein/boxen, and edit this url to your own repository.
rm /etc/ltsp/dhcp.conf
git init
git remote add origin https://github.com/jphein/boxen
git pull https://github.com/jphein/boxen/etc/ltsp/ltsp-build-client.conf
ltsp-build-client --fatclient
git pull origin master
ltsp-update-image
sudo gluster peer probe boxen2
sudo gluster volume create vms replica 2 transport tcp boxen1:/vms boxen2:/vms force
sudo gluster volume create vms replica 2 transport tcp boxen1:/storage boxen2:/storage force
mkdir /mnt/vms-pool /mnt/storage-pool
#Bridge

```

To install on the second server or for a headless install: 
PXE boot using existing boXen or LTSP server: 

Add to your /etc/ltsp/dhcpd.conf
```sh
[<mac address>]
 filename /ubuntu-installer/amd64/pxelinux.0
```
Then
ssh ubuntu@<ip from dhcp syslog> -p ubuntu 
Then run the above steps as if you were installing with CD

You many want to run this command after boXenLinux is installed to enable a firewall.
CAUTION: You need to setup rules first. This could disconnect you, if you are using SSH to install.
```sh
sudo ufw enable
```
[//]: # (These are reference links used in the body of this note and get stripped out when the markdown processor does its job. There is no need to format nicely because it shouldn't be seen. Thanks SO - http://stackoverflow.com/questions/4823468/store-comments-in-markdown-syntax)

The registered trademark Linux® is used pursuant to a sublicense from the Linux Foundation, the exclusive licensee of Linus Torvalds, owner of the mark on a world-wide basis.

[git]: <https://github.com>
[KVM-VDI]: <https://github.com/Seitanas/kvm-vdi>  
[LTSP]: <https://github.com/gentoo-mirror/ltsp>
[jp]: <https://github.com/jphein>
[boxen]: <https://github.com/jphein/boxen>
[Ubuntu]: <http://www.ubuntu.com/download/server>
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
