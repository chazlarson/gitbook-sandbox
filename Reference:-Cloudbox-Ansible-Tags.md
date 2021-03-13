Reference of the Ansible tags you can run on CB. 

For an updated list of what they are, run the following:

```
sudo ansible-playbook cloudbox.yml --list-tags 2>&1 | grep "TASK TAGS" | cut -d":" -f2 | awk '{sub(/\[/, "")sub(/\]/, "")}1' | sed -e 's/,//g' | xargs -n 1 | sort -u
```



# Command

```
sudo ansible-playbook cloudbox.yml --tags <TAG>
```


# Major Tags

| Ansible Tags | Function                     |
|:------------ |:---------------------------- |
| `cloudbox`   | Install/Update Full Cloudbox |
| `feederbox`  | Install/Update Feederbox     |
| `mediabox`   | Install/Update Mediabox      |
| `backup`     | Backup Cloudbox              |
| `restore`    | Restore Cloudbox Backup      |
| `kernel`     | Update the Kernel            |


# Default Tasks

| Ansible Tags    | Function                                |
|:--------------- |:--------------------------------------- |
| `ctop`          | Reinstall/Update Ctop                   |
| `hostess`       | Reinstall/Update Hostess                |
| `jackett`       | Reinstall/Update Jackett                |
| `motd`          | Reinstall/Update Cloudbox Motd          |
| `nginx-proxy`   | Reinstall/Update Nginx-Proxy            |
| `ngrok`         | Reinstall/Update Ngrok                  |
| `nzbget`        | Reinstall/Update NZBGet                 |
| `nzbhydra`      | Reinstall/Update NZBHydra               |
| `nzbhydra2`     | Reinstall/Update NZBHydra2              |
| `ombi`          | Renstall/Update Ombi                     |
| `organizr`      | Reinstall/Update Organizr               |
| `plex`          | Reinstall/Update Plex                   |
| `plex_autoscan` | Reinstall/Update Plex Autoscan          |
| `plexpy`        | Reinstall/Update PlexPy (Tautulli)      |
| `portainer`     | Reinstall/Update Portainer              |
| `radarr`        | Reinstall/Update Radarr                 |
| `rclone`        | Reinstall/Update Rclone                 |
| `rutorrent`     | Reinstall/Update ruTorrent              |
| `scripts`       | Reinstall/Update Scripts folder         |
| `settings`      | Update config files (*.yml) with new/updated variables. |
| `sonarr`        | Reinstall/Update Sonarr                 |
| `cloudplow`     | Reinstall/Update Cloudplow              |



# Addon Apps

| Ansible Tags      | Function                       |
|:----------------- |:------------------------------ |
| `emby`            | Install/Update Emby            |
| `heimdall`        | Install/Update Heimdall        |
| `lidarr`          | Install/Update Lidarr          |
| `netdata`         | Install/Update Netdata         |
| `nextcloud`       | Install/Update Nextcloud       |
| `nzbhydra2`       | Install/Update NZBHydra2       |
| `ombi`            | Install/Update Ombi            |
| `plex_dupefinder` | Install/Update Plex Dupefinder |
| `plex_patrol`     | Install/Update Plex Patrol     |
| `plexrequests`  | Reinstall/Update Plex Requests - Meteor |
| `quassel`         | Install/Update Quassel         |
| `resilio`         | Install/Update Resilio Sync    |
| `thelounge`       | Install/Update The Lounge      |
| `traktarr`        | Install/Update Traktarr        |
| `watchtower`      | Install/Update Watchtower      |
| `znc`             | Install/Update ZNC             |
| `shell`           | Swap Shells: bash <--> zsh     |
