## What is UnionFS Cleaner?

### Uploader Function
[UnionFS Cleaner](https://github.com/l3uddz/unionfs_cleaner) is a script by [l3uddz](https://github.com/l3uddz) that moves all the content in `/mnt/local/Media/` (see [[Paths|Basics: Cloudbox Paths#unionfs_cleaner]]) to cloud storage (e.g. Google Drive) after the folder reaches a size threshold. This was first set during initial install of Cloudbox via the [[settings.yml|Install: Settings]] file, but can also be changed later (see below). 


_UnionFS Cleaner comes preset with default configuration as related to Cloudbox, and as such, requires no configuration out of the box, for most users. However, on this page mentions a couple configuration settings you may use to customize UnionFS Cleaner._


### Cleaner Function

On top of uploading your media files to the cloud storage, UnionFS Cleaner functions as a UnionFS whiteout file (i.e. `*_HIDDEN~`) cleaner.

When Sonarr & Radarr upgrade your media files, they attempt delete the previous ones. When that data is still on the local server, it is deleted immediately, but when it has been moved to Google Drive, it is unable to do so because the Google Drive mount is set as read-only (via Plexdrive). Instead, UnionFS will create a whiteout file (a blank file in the format of `filename.ext_HIDDEN~`) that makes the file invisible to whatever tries to access it via the UnionFS mount (.e.g. `/mnt/unionfs/`) and, therefore, Sonarr & Radarr will consider the file deleted, however, the media file will still exist on the cloud.

To resolve this, on the next upload task (i.e. when size threshold is reached on the next interval check), UnionFS Cleaner will scan for the whiteout file(s), remove the corresponding media file from the cloud storage, then remove the whiteout file (since it isn't needed anymore), and as a result, keep your content free of duplicates.



### Google Drive Ban Sleep

Recently, Google Drive has implemented a max upload of ~750GB per day. When this limit is reached, Google Drive will put you in a 24 hour soft ban. When UnionFS Cleaner encounters this (as "Error 403: User Rate Limit Exceeded"), it will go into a 25 hour ban sleep, and upon waking up, will resume checking and uploading tasks. This is so much better than having a Rclone task running all day long with the bwlimit set at 8M. To see what this looks like, checkout the screenshot below.


_To learn more about UnionFS Cleaner and all the options available, see [https://github.com/l3uddz/unionfs_cleaner](https://github.com/l3uddz/unionfs_cleaner)._



## UnionFS Cleaner Config




### Default config.json file

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




### Modify Upload Threshold and Interval


1. On the server's shell, run the following command:

    ```
    nano /opt/unionfs_cleaner/config.json
    ```

1. Set `"local_folder_check_interval":` to specify the interval (in min) UnionFS Cleaner checks the size of local_folder (i.e. /mnt/local/Media).

   - Note: Make sure there is a comma (`,`) at the end.

1. Set `"local_folder_size":` to specify the max size, in GB (but not less than 2GB), UnionFS Cleaner will allow the local_folder (i.e. /mnt/local/Media) to get before initiating an upload/move to Google Drive.

   - Note: Make sure there is a comma (`,`) at the end.

1. `Ctrl-x`, `y`, and `enter` to save.

1. UnionFS Cleaner will restart itself when it detects config.json has changed.


### Enable Pushover Notifications


Notifications will be sent when UnionFS Cleaner..
- begins an upload task.
- skips an upload task due to files being accessed.
- is put into a 25 hour ban sleep.
- is restored after the ban sleep.

To enable Pushover notifications, click [[here|Pushover#unionfs-cleaner]].


<img src="https://i.imgur.com/hiriDUc.png">
