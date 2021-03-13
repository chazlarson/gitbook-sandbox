# Apps

## Backups

Logs are stored in `~/logs`.

### Previous Backups:

```
cat ~/logs/cloudbox_backup-<DATE>.log
```

### Current Backup:

```
tail -F ~/logs/cloudbox_backup-<DATE>.log
```


## Plex Autoscan


### Check Status:
```
sudo systemctl status plex_autoscan.service
```

### Restart Service:
```
sudo systemctl restart plex_autoscan.service
```

### Previous Activity:

```
cat /opt/plex_autoscan/plex_autoscan.log
```

Older logs are named as plex_autoscan.log.1, plex_autoscan.log.2, etc.

### Live Log:
```
tail -F /opt/plex_autoscan/plex_autoscan.log
```
or
```
sudo journalctl -o cat -fu plex_autoscan.service
```

## Cloudplow


### Check Status:
```
sudo systemctl status cloudplow.service
```

### Previous Activity:

```
cat /opt/cloudplow/cloudplow.log
```

Older logs are named as cloudplow.log.1, cloudplow.log.2, etc.

### Live Log:
```
tail -F /opt/cloudplow/cloudplow.log
```
or
```
sudo journalctl -o cat -fu cloudplow.service
```



# Remote Mount

Pick one of these.

## Rclone VFS

### Check Status:
```
sudo systemctl status rclone_vfs.service
```

### See a live log:
```
sudo journalctl -o cat -fu rclone_vfs.service
```

## Rclone Cache

### Check Status:
```
sudo systemctl status rclone_cache.service
```

### See a live log:
```
sudo journalctl -o cat -fu rclone_cache.service
```

## Plexdrive 4

### Check Status:
```
sudo systemctl status plexdrive4.service
```

### See a live log:
```
sudo journalctl -o cat -fu plexdrive4.service
```

## Plexdrive 5

### Check Status:
```
sudo systemctl status plexdrive5.service
```

### See a live log:
```
sudo journalctl -o cat -fu plexdrive5.service
```

# Union Mount

Pick one of these.

## MergerFS

### Check Status:
```
sudo systemctl status mergerfs.service
```

### See a live log:
```
sudo journalctl -o cat -fu mergerfs.service
```

## UnionFS

### Check Status:
```
sudo systemctl status unionfs.service
```

### See a live log:
```
sudo journalctl -fu unionfs.service
```





# Docker

Find the container name: `docker ps -a`

## Live logs

### Live log (from the beginning of the log):
```
docker logs --follow <container_name>
```

### Live log (from the last 10 lines of the log):
```
docker logs --follow --tail 10 <container_name>
```


### Examples:

```
docker logs -f plex
```

Note: `--follow` = `-f`


## Let's Encrypt

In addition to the above, you may use the following commands to display info about your existing certificates.


### Cert Status

```
docker exec letsencrypt /app/cert_status
```

### Logs

```
docker logs -f letsencrypt
```