# boXenLinux&copy;- A redundant Linux distribution based on Ubuntu for nonprofits. 
Open source zeroclient VDI project based on Ubuntu Linux [LTSP] and [KVM-VDI]
[LTSP] provides thinclient driven session based remote desktop for:
Linux, Windows, and MacOS using ldm, xfreerdp, and xtightvncviwer respectively.
It also, provides fatclients for Ubuntu Desktop.
[KVM-VDI] provides VDI based remote desktop for all OS's using KVM and Spice.
It uses GlusterFS for clustered storage and CTDB for shares.

Requirements: Two real metal computers. 

To install use an [Ubuntu LiveCD for Ubuntu 16.04 Server][Ubuntu]. Then run the below in a root terminal.

```sh
apt-get install git #To install packages.
git clone https://github/jphein/boxen /   #To download and install configs. To have your own configs installed. Fork jphein/boxen, and edit this url to your own repository.
```
Or,
Use the custom ISO: <isolink>

Roadmap: Have an Ubuntu cloud version for large nonprofits with 6 servers or more.

You many want to run this command after boXenLinux is installed to enable a firewall.
CAUTION: You need to setup rules first. This could disconnect you, if you are using SSH to install.
```sh
ufw enable
```
[//]: # (These are reference links used in the body of this note and get stripped out when the markdown processor does its job. There is no need to format nicely because it shouldn't be seen. Thanks SO - http://stackoverflow.com/questions/4823468/store-comments-in-markdown-syntax)

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
