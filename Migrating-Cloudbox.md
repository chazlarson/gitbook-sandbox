This guide will outline some basic steps to copy/move your Cloudbox setup to another server and/or another domain name.

Listed below are some common scenarios and their migration instructions. 

## Move Cloudbox to Another Server and Keep the Same Domain Name

### Previous Server

1. [Backup](Cloudbox-Backup-and-Restore#cloudbox-backup) your current Cloudbox server.


### New Server

1. [Restore](Cloudbox-Backup-and-Restore#cloudbox-restore) Cloudbox to the new server (skip steps #7 and #8 for now).

1. If you are not using Cloudflare: 

   - Point your domain's [[DNS|Prerequisites: Domain Name]] to the new server.

1. Install the relevant Cloudbox type: [[Cloudbox|Install: Cloudbox]], [[Mediabox|Install: Mediabox]], or [[Feederbox|Install: Feederbox]] (step #7 of the [Restore](Cloudbox-Backup-and-Restore#cloudbox-restore) instructions).

1. Install any extra, not-default containers you had installed previously (step #8 of the [Restore](Cloudbox-Backup-and-Restore#cloudbox-restore) instructions).

1. Check to see if your [[Plex Autoscan URL|Install: Plex Autoscan#3-obtaining-the-plex-autoscan-url]] has changed and update [[Sonarr|Install: Sonarr#plex-autoscan]], [[Radarr|Install: Radarr#plex-autoscan]], and [[Lidarr|Install: Lidarr#plex-autoscan]], accordingly. 

## Move Cloudbox to Another Server and Change the Domain Name

### Previous Server


1. [Backup](Cloudbox-Backup-and-Restore#cloudbox-backup) your current Cloudbox server.

1. [[Revoke|Revoking SSL Certificates]] your domain's SSL certificates.<sup name="a1">[\[1\]](#f1) </sup>


### New Server 

1. [Restore](Cloudbox-Backup-and-Restore#cloudbox-restore) Cloudbox to the new server (skip steps #7 and #8 for now).

1. Add in your new domain name into [[settings|Install: Settings]].

1. If you are using Cloudflare: 

   1. Register your domain with [[Cloudflare|Prerequisites: Cloudflare]].

   2. Add the Cloudflare API into [[settings|Install: Settings]].

1. If you are not using Cloudflare: 

   - Point your new domain's [[DNS|Prerequisites: Domain Name]] to the new server.

1. Replace the domain name in app specific config files:

   - `/opt/cloudplow/config.json`

   - `/opt/emby/config/system.xml` (only if installed)

   - `/opt/motd/config.json`

   - `/opt/traktarr/config.json` (only if installed)

   - `/opt/plex_dupefinder/config.json` (only if installed)

   - `/opt/plex_patrol/settings.ini` (only if installed)

   - `/opt/sabnzbd/app/sabnzbd.ini` (only if installed)

1. Install the relevant Cloudbox type: [[Cloudbox|Install: Cloudbox]], [[Mediabox|Install: Mediabox]], or [[Feederbox|Install: Feederbox]] (step #7 of the [Restore](Cloudbox-Backup-and-Restore#cloudbox-restore) instructions).

1. Install any extra, not-default containers you had installed previously (step #8 of the [Restore](Cloudbox-Backup-and-Restore#cloudbox-restore) instructions).

1. Check to see if your [[Plex Autoscan URL|Install: Plex Autoscan#3-obtaining-the-plex-autoscan-url]] has changed and update [[Sonarr|Install: Sonarr#plex-autoscan]], [[Radarr|Install: Radarr#plex-autoscan]], and [[Lidarr|Install: Lidarr#plex-autoscan]], accordingly. 


## Keep Cloudbox on the Same Server but Change the Domain Name

1. [Backup](Cloudbox-Backup-and-Restore#cloudbox-backup) your current Cloudbox server (Optional, but recommended).

1. [[Revoke|Revoking SSL Certificates]] your domain's SSL certificates.<sup name="a1">[\[1\]](#f1) </sup>

1. Add in your new domain name into [[settings|Install: Settings]].

1. If you are using Cloudflare: 

   1. Register your domain with [[Cloudflare|Prerequisites: Cloudflare]].

   2. Add the Cloudflare API into [[settings|Install: Settings]].

1. If you are not using Cloudflare: 

   - Point your new domain's [[DNS|Prerequisites: Domain Name]] to the server.

1. Replace the domain name in app specific config files:

   - `/opt/cloudplow/config.json`

   - `/opt/emby/config/system.xml` (only if installed)

   - `/opt/motd/config.json`

   - `/opt/traktarr/config.json` (only if installed)

   - `/opt/plex_dupefinder/config.json` (only if installed)

   - `/opt/plex_patrol/settings.ini` (only if installed)

   - `/opt/sabnzbd/app/sabnzbd.ini` (only if installed)

1. Install the relevant Cloudbox type: [[Cloudbox|Install: Cloudbox]], [[Mediabox|Install: Mediabox]], or [[Feederbox|Install: Feederbox]] (step #7 of the [Restore](Cloudbox-Backup-and-Restore#cloudbox-restore) instructions).

1. Install any extra, not-default containers you had installed previously (step #8 of the [Restore](Cloudbox-Backup-and-Restore#cloudbox-restore) instructions).

1. Check to see if your [[Plex Autoscan URL|Install: Plex Autoscan#3-obtaining-the-plex-autoscan-url]] has changed and update [[Sonarr|Install: Sonarr#plex-autoscan]], [[Radarr|Install: Radarr#plex-autoscan]], and [[Lidarr|Install: Lidarr#plex-autoscan]], accordingly. 

1. Remove any files that contain your domain name in `/opt/nginx-proxy/vhost.d`. nginx will re-generate them automatically for your new domain. maually change the contents of any file in `/opt/nginx-proxy/conf.d` to point to your new domain. Not doing either of these steps will cause nginx to have issues restarting and will lead to "Page cannot be found" errors when attempting to browse to your services. 



---


<sup><b name="f1">[1](#a1)</b> This will free up the domain name from Let’s Encrypt and you will be able to use it in the future without having to wait for the previous certificates to expire (~90 days). </sup>