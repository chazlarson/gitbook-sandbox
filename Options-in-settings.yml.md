
**Note:** Having `{{user}}` in the path tells Ansible to fill in the username, automatically. You do not need to fill in your actual username.

---

- `downloads`: Where downloads go.

    - `nzbs`: Path for Usenet app downloads. 
  
      - Default is `/mnt/local/downloads/nzbs`.

       - Example: With the default path, NZBGet downloads would go to `/mnt/local/downloads/nzbs/nzbget/completed`, where as, SABnzbd downloads would go to `/mnt/local/downloads/nzbs/sabnzbd/complete`.

    - `torrents`: Path for BitTorrent app downloads. 

        - Default is `/mnt/local/downloads/torrents`.

       - Example: With the default path, ruTorrent downloads would go to `/mnt/local/downloads/torrents/rutorrent/completed`.

- `plex`: Plex options.

   - `tag`: Determines what version of Plex to install. 


     - Options are `public`, `beta`, or [[version tag|https://hub.docker.com/r/cloudb0x/plex/tags]] (e.g. `"1.12.3.4973-215c28d86"`). 

     - Default is `public`.

     - Notes:

       - Note 1: The `public` tag restricts this check to public versions only, where as, `beta` tag will fetch beta versions. If the server is not logged in or you do not have an active [Plex Pass](https://www.plex.tv/features/plex-pass/) on your Plex account, the `beta` tag will only install the publicly available versions only. 

       - Note 2: Hardware Transcoding requires an  active [Plex Pass](https://www.plex.tv/features/plex-pass/). This can be enabled on either the `public` or `beta` tagged versions. 

       - Note 3: If you decide to change the tags later, you will need to update Plex by running the Cloudbox install command with the "plex" tag (i.e. `sudo ansible-playbook cloudbox.yml --tags plex`).

  - `transcodes`: Path of temporary transcoding files. 

     - Default is `"/mnt/local/transcodes"`.

    - Note: It is recommended to **not** use `/tmp` or `/dev/shm` as a transcode location because the paths are cleared on reboots, causing Docker to create the folder as root and Plex transcoder to crash. Another reason why not to: [https://forums.plex.tv/discussion/comment/1502936/#Comment_1502936](https://forums.plex.tv/discussion/comment/1502936/#Comment_1502936).

- `rclone`: Rclone options.

  - `version`: Rclone version that is installed by Cloudbox. 

     - Choices are `latest` (or `current`), `beta`, or a specific version number (e.g. `1.42`). 

     - Default is `latest`.

  - `remote`: Rclone remote that Cloudbox will use to setup Rclone VFS mount and Cloudplow. 

     - Default is `google`.

- `shell`: Type of shell to use. 

   - Choices are `bash` or `zsh`. 

   - Default is `bash`.
