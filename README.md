# seedbox
Full mediacenter server based on Docker containers

## Description

This is project aims to deploy all services needed to configure a seedbox 
(based on Linux Debian 8) as a full mediacenter.

All the services run into Docker containers

- Muximux is used to provide a single web interface to all services
- Plex server is used for the mediacenter
- Sonarr and Radarr are used to get TV Shows and Movies into Plex
- Transmission is used as a torrent downloader for Sonarr and Radarr
- RuTorrent is used to manually downloading torrents
- Jackett is used to configure Indexers for Sonarr/Radarr
- FlexGet is used to periodically clean Transmission queues
- PlexPy is used for monitoring Plex server and Notifications (ie. on Slack channels)
- Glances is used for monitoring the server
- Fail2Ban is used to prevent DOS attacks


## Installation

Requires : 
 - Server running Debian 8
 - Ansible 2.4 or newer
 - Git
		   
The project uses an Ansible playbook to automate the installation of the services.

The Ansible playbook can be used to install the services on a local server or
a on remote server.

----------
To install Git :

	$ apt-get install git
	
----------
To install Ansible : 
 
Add the following line to /etc/apt/sources.list:

	deb http://ppa.launchpad.net/ansible/ansible/ubuntu trusty main

Then run these commands:

     $ sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 93C4A3FD7BB9C367
     $ sudo apt-get update
     $ sudo apt-get install ansible
     
----------
To download Git project
    
	$ git clone https://github.com/rmanus/seedbox.git

---------
Edit groups_vars/all
 
Adjust the following parameters :
  
	timezone
	server_ip  		(this is the public ip address of the mediaserver)
	flexget_passwd 	(required to connect to flexget WebUI)
	plex_claim 		(The claim token for the server to obtain a real server token. 
				If not provided, server is will not be automatically logged in. 
				If server is already logged in, this parameter is ignored. 
				You can obtain a claim token to login your server to your plex 
				account by visiting https://www.plex.tv/claim )
			  
Execute Ansible playbook (on local host)
 
	$ sudo ansible-playbook -i "localhost," -c local site.yml
  
Connect to WebUI
 
	http://<public_ip_address>
  
## Dependencies

This project depends on the following docker images

- [linuxserver/muximux](https://hub.docker.com/r/linuxserver/muximux)
- [plexinc/pms-docker](https://hub.docker.com/r/plexinc/pms-docker)
- [linuxserver/transmission](https://hub.docker.com/r/linuxserver/transmission)
- [linuxserver/jackett](https://hub.docker.com/r/linuxserver/jackett)
- [linuxserver/radarr](https://hub.docker.com/r/linuxserver/radarr)
- [linuxserver/sonarr](https://hub.docker.com/r/linuxserver/sonarr)
- [linuxserver/ombi](https://hub.docker.com/r/linuxserver/ombi)
- [linuxserver/rutorrent](https://hub.docker.com/r/linuxserver/rutorrent)
- [linuxserver/plexpy](https://hub.docker.com/r/linuxserver/plexpy/)
- [nicolargo/glances](https://hub.docker.com/r/nicolargo/glances/)
- [cpoppema/docker-flexget](https://hub.docker.com/r/cpoppema/docker-flexget/)
- [superitman/fail2ban](https://hub.docker.com/r/superitman/fail2ban)
