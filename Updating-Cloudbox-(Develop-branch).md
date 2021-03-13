You can use this guide to keep up with new additions/changes with Cloudbox.

### Foreword

- You will not lose your existing data (e.g. Plex libraries, Sonarr/Radarr db, configs, etc) as that is stored in `/opt`.

- The follow settings files will remain intact: 

  - `ansible.cfg`
  - `accounts.yml`
  - `settings.yml`
  - `adv_settings.yml`
  - `backup_config.yml`
  - `backup_excludes.txt` (if it exists)

- Since Docker itself may be updated during this process, some non-Cloudbox docker containers _may_ either get stopped or removed during this process, but their persistent config data should remain intact. 




### Update Cloudbox

1. Pull the latest changes to the repo.

   ```bash
   cb update
   ```

1. Run the Cloudbox installer with your preferred [[tag|Basics:-Cloudbox-Install-Types]] (`cloudbox`, `mediabox`, or `feederbox`). Add any "non-default" roles onto the list of tags, separated by a comma. 
   
   Examples:

   ```bash
   cb install cloudbox
   ```

   ```bash
   cb install cloudbox,emby,plexrequests
   ```

   _Note: Install may quit if new changes were added into any of the `.yml` files (e.g. `settings.yml`) via the [[Settings Updater]] role. If this happens, check the the updated `.yml` file for the new additions and re-start the install._


1. Reboot when the install completes.

   ```bash
   sudo reboot
   ```