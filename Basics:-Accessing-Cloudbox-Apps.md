

_Note 1: After the initial setup, it will take a a while for the SSL certificates to propagate. A side effect of this will be that certain domains were redirect to other apps (e.g. sonarr.yourdomain.com -> nzbget.yourdomain.com). Just give it a bit of time and this will correct itself._

_Note 2: If pages don't load at all, make sure [[setup|Prerequisites: Domain Name]] your domain properly and also checkout the [[FAQ|FAQ#nginx-proxy]]._


## Default Apps

Cloudbox apps will be accessed via appname._yourdomain.com_ (see table below).

| **App  Name**          | **URL**                               |
|:---------------------- |:------------------------------------- |
| Jackett                | https://jackett._yourdomain.com_      |
| NZBGet                 | https://nzbget._yourdomain.com_       |
| NZBHydra2              | https://nzbhydra2._yourdomain.com_    |
| Organizr               | https://organizr._yourdomain.com_     |
| Plex                   | https://plex._yourdomain.com_         |
| WebTools for Plex*     | http://plex._yourdomain.com_:33400    | 
| Plexpy (Tautulli)      | https://plexpy._yourdomain.com_       |
| Plex Requests          | https://plexrequests._yourdomain.com_ |
| Portainer              | https://portainer._yourdomain.com_    |
| Radarr                 | https://radarr._yourdomain.com_       |
| ruTorrent              | https://rutorrent._yourdomain.com_    |
| Sonarr                 | https://sonarr._yourdomain.com_       |

\* Use http://_youripaddress_:33400 if that does not work. 



## Additional Apps

Coming soon.