##  Overview of Settings ##


```yaml
---
user: seed
passwd: password123
domain: testcloudbox.ml
email: your@email.com
cloudflare_api_token:
nzbget:
  downloads: /mnt/local/downloads/nzbget
rutorrent:
  downloads: /mnt/local/downloads/rutorrent
plex:
  tag: public
  transcodes: /home/{{user}}/transcodes
rclone:
  version: latest
backup:
  tar_dest: /home/{{user}}/Backups
  rsync_dest: rsync://somehost.com/Backups
  rclone_dest: google:/Backups
  keep_local_copy: true
  use_rsync: false
  use_rclone: false
  cron_time: weekly
  cron_state: absent
  pushover_app_token:
  pushover_user_key:
```