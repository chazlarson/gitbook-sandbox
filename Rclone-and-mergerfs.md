## Rclone mount
```
[Unit]
Description=rclone mount
# Depend on network
Requires=network-online.target
After=network-online.target
# Check directories
AssertPathIsDirectory=<rclone_mount_path>

[Service]
Type=notify

User=data
Group=data

# Mount command
ExecStart=/usr/local/bin/rclone mount \
  --config=<config_path>/.rclone.conf \
  --allow-other \
  --rc \
  --fast-list \
  --drive-skip-gdocs \
  --vfs-read-chunk-size=64M \
  --vfs-read-chunk-size-limit=2048M \
  --buffer-size=64M \
  --max-read-ahead=256M \
  --poll-interval=1m \
  --dir-cache-time=168h \
  --timeout=10m \
  --transfers=16 \
  --checkers=12 \
  --drive-chunk-size=64M \
  --fuse-flag=sync_read \
  --fuse-flag=auto_cache \
  --umask=002 \
  --syslog \
  -v \
  <remote>:<root_path> <rclone_mount_path>

# Unmount on stop
ExecStop=/bin/fusermount -uz <rclone_mount_path>
Restart=on-abort
RestartSec=5
StartLimitInterval=60s
StartLimitBurst=3

[Install]
WantedBy=default.target
```

## mergerfs mount
```
[Unit]
Description=mergerfs mount

Requires=<rclone_service>
After=<rclone_service>

AssertPathIsMountPoint=<rclone_mount_path>
AssertPathExists=<rclone_mount_path>/<check_file>

[Mount]
What=<local_mount>:<rclone_mount_path>
Where=<overlay_mount>
Type=fuse.mergerfs
Options=defaults,category.create=ff,minfreespace=0,allow_other,dropcacheonclose=true,security_capability=false,xattr=nosys,statfs_ignore=ro,use_ino,hard_remove,auto_cache,sync_read,umask=0002,noatime

[Install]
WantedBy=default.target
```