The Develop branch installs a helper script as `cb`.

This script is intended to provide shortcuts for common tasks.

Currently it can be used to run cloudbox roles and update the cloudbox repo.

```
Usage:
    cb [-h]                Display this help message.
    cb install <package>   Install <package>.
    cb update              Update Cloudbox project folder.
```

Using this script, you can run:
```
cb install SOMETAG
```
instead of:
```
cd ~/cloudbox && sudo ansible-playbook cloudbox.yml --tags SOMETAG
```

Also:
```
cb update
```
instead of:
```
cd ~/cloudbox && git fetch && git reset --hard @{u}
```

You can run this helper from anywhere; you don't have to cd into the cloudbox directory first.

### "ArrX" functionality

For some tags, the script can install an instance of a container with an arbitrary name:

```
cb install plex -e plex_name=plex_bing
```
would install a `plex_bing` container that stores its data in `/opt/plex_bing` and is accessible at `https://plex_bing.DOMAIN.TLD`.

Current roles that support this feature are:
```
cloudplow
emby
jackett
lidarr
mariadb
netdata
nzbget
nzbhydra2
ombi
plex
portainer
radarr
rutorrent
sabnzbd
sonarr
sstvirl
tautulli
trackarr
```
