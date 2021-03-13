```yaml
---
system:
  timezone: auto
```
Set a timezone, or let cloudbox set it for you.

```yaml
docker:
  repo: edge
  version: latest
```

```yaml
mounts:
  unionfs: mergerfs
  remote: rclone_vfs
```
Choose mergerfs or unionfs, rclone_vfs, rclone_cache or plexdrive 4/5

```yaml
plex:
  open_main_ports: no
  open_extra_ports: no
  force_auto_adjust_quality: no
  force_high_output_bitrates: no
  db_cache_size: default
```
Adjust various Plex settings.

```yaml
suitarr:
  version: default
```
No longer used.

```yaml
sonarr:
  version: v3
```
No longer used.

```yaml
darkerr:
  enable: no
```
Install Darkerr theme for Radarr, Sonarr, and nzbget

```yaml
emby:
  version: latest
```
Choose version of emby; this must be a tag from [embyserver on dockerhub](https://hub.docker.com/r/emby/embyserver/tags)

```yaml
organizr:
  direct_domain: no
```
If `direct_domain: yes` organizr will be available at your base domain: DOMAIN.TLD rather than organizr.DOMAIN.TLD

```yaml
nginx:
  direct_domain: no
  subdomain: web
```
If `direct_domain: yes` a website will be available at your base domain: DOMAIN.TLD
If `direct_domain: no` a website will be available at the specified subdomain: web.DOMAIN.TLD

After making changes here run the `nginx` tag to make them take effect.

```yaml
ombi:
  subdomain: ombi
```
Subdomain you want to use for ombi.

```yaml
sickbeard_mp4_automator: no
```
Set up the Sickbeard MP4 automator in the relevant apps.

NOTE: Due to image changes this currently has problems.

```yaml
gpu:
  intel: yes
  nvidia:
    enabled: no
    driver: 418.30
```
Settings for hardware transcoding in Plex.

After making changes here run the `plex` tag to make them take effect.

```yaml
hetzner_nfs:
  vlan_id: 4000
  mount_client: 3
```
Settings for the `hetzner_nfs` role.


NOTE: generally speaking, all of these settings will require some tags to be rerun to take effect.  For example, if you turn Darkerr on, nothing's going to change until you rerun the Radarr, Sonarr, or nzbget tags.
