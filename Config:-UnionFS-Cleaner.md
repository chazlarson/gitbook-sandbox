```json

{
    "cloud_folder": "/mnt/plexdrive",
    "dry_run": false,
    "du_excludes": ["*.partial~"],
    "local_folder": "/mnt/local/Media",
    "local_folder_check_interval": 30,
    "local_folder_size": 200,
    "local_remote": "google:/Media",
    "lsof_excludes": [
        ".partial~"
    ],
    "pushover_app_token": "",
    "pushover_user_token": "",
    "rclone_bwlimit": "",
    "rclone_checkers": 16,
    "rclone_chunk_size": "8M",
    "rclone_excludes": [
        "**partial~",
        "**_HIDDEN",
        ".unionfs/**",
        ".unionfs-fuse/**"
    ],
    "rclone_remove_empty_on_upload": {
        "/mnt/local/Media/Movies": 1,
        "/mnt/local/Media/TV": 1
    },
    "rclone_transfers": 8,
    "remote_folder": "google:",
    "unionfs_folder": "/mnt/local/.unionfs-fuse",
    "use_config_manager": true,
    "use_git_autoupdater": true,
    "use_upload_manager": true
}
```