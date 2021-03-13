<!-- TOC depthFrom:1 depthTo:6 withLinks:1 updateOnSave:0 orderedList:0 -->

- [Intro](#intro)
- [Cloudbox Backup](#cloudbox-backup)
- [Cloudbox Restore](#cloudbox-restore)


<!-- /TOC -->

---



# Intro

Backup and Restore is a built-in feature of Cloudbox that makes it easy to back-up your entire Cloudbox setup, with the ability to restore it anywhere.

_Note 1: Only app data located in '/opt' and relevant config files are backed up. For more details, see [here](FAQ#what-is-backed-up)._

_Note 2: If you wish to move your Cloudbox to another server via Backup / Restore, see [[Migrating Cloudbox]]._

# Cloudbox Backup

**Cloudbox Backup** backs up the Docker container app data (i.e. `/opt`), and all relevant config files, and uploads it to an Rclone or Rsync remote (if they are enabled).

Backup can be ran manually (steps below), for an immediate, one-time backup, or [[scheduled|Cloudbox Backup and Restore Scheduling]] to run periodically.

_Note: During backup, all Cloudbox managed Docker containers will be shut down  (i.e. Plex will be unavailable) while the tarball files are being made._


Steps to run a manual backup:

**Master branch**

1. Go into your Cloudbox folder

   ```shell
   cd ~/cloudbox
   ```

2. Make sure backup settings (i.e. [[backup_config.yml|Cloudbox Backup and Restore Settings]]) are filled out.

3. Run the backup command

   ```shell
   sudo ansible-playbook cloudbox.yml --tags backup
   ```

   via screen:


   ```shell
   screen -dmS cloudbox-backup sudo ansible-playbook cloudbox.yml --tags backup
   ```

   ```shell
   screen -r
   ```

   ```shell
   CTRL A + D
   ```

**Develop branch**

1. Make sure backup settings (i.e. [[~/cloudbox/backup_config.yml|Cloudbox Backup and Restore Settings]]) are filled out.

3. Run the backup command

   ```shell
   cb install backup
   ```

   via screen:


   ```shell
   screen -dmS cloudbox-backup cb install backup
   ```

   ```shell
   screen -r
   ```

   ```shell
   CTRL A + D
   ```

For scheduled backups, see [[here|Cloudbox Backup and Restore Scheduling]].

If for some reason your backup stops/ you accidentally reboot the server etc.: You'll need to remove the backup.lock file in your cloudbox directory, otherwise tags will not run. 

# Cloudbox Restore

**Cloudbox Restore** downloads the backup from the cloud (if Rclone or Rsync were enabled) and restores it to the `/opt` folder (this is done automatically and requires no manual intervention). 

If a local backup (e.g. `/opt` tarball files) already exists in the backup folder, those tarball files will be used instead. 

Backup can be restored on the same server or brand new one, with everything exactly as you left it at the time of backup. See [[Migrating Cloudbox]] for more info.

Steps below assume you are restoring to a new / wiped server.

1. Install [[dependencies|Install: Dependencies]] and download the Cloudbox project repository.

1. If the Restore Service was enabled in [[settings|Cloudbox-Backup-and-Restore-Settings]] (i.e.  <code>restore_service</code> credentials were supplied in [[backup_config.yml|Cloudbox-Backup-and-Restore-Settings]]), you will be able automatically restore the config files into the `~/cloudbox` folder. 

   To do so run the following command (replace `USERNAME` and `PASSWORD` with your `restore_service` credentials).

   ```
   curl -s https://cloudbox.works/scripts/restore.sh | bash -s 'USERNAME' 'PASSWORD'
   ```
   NOTE: Wrap your USERNAME and PASSWORD in quotes just as shown there.

   NOTE: These are not [necessarily] your login credentials.  This is a username/password that **you have to enter yourself** in the backup_config.yml file.  **The Cloudbox install does not automatically fill these in**.  If you did not fill these in yourself, then the Cloudbox Restore Service is *NOT* enabled.

1. <details><summary>If the Cloudbox Restore Service was not enabled (i.e. <code>restore_service</code> credentials were NOT supplied in [[backup_config.yml|Cloudbox-Backup-and-Restore-Settings]])... (CLICK TO EXPAND)</summary> <br/>
   <ul>
     <li>Find the following files in your backup and drop them into the <code>~/cloudbox</code> folder:</li> <br/>
         <ul>
         <li><code>ansible.cfg</code></li> <br/>
         <li><code>accounts.yml</code></li> <br/>
         <li><code>settings.yml</code></li> <br/>
         <li><code>adv_settings.yml</code></li> <br/>
         <li><code>backup_config.yml</code></li> <br/>
         <li><code>rclone.conf</code></li> </ul><br/>
   <li><i>Note 1: These files were backed up separately from the backup tarball files so they can easily be copied here.</i></li> <br/>
   <li><i>Note 2: During the restore process, the <code>rclone.conf</code> file will be moved to <code>~/.config/rclone/rclone.conf</code>.</i></li> <br/>
   <li><i>Note 3: The <code>/opt</code> folder gets downloaded/restored automatically in the next step, and doesn’t require manual downloading or unpacking.</i></li> <br/>
   </ul>
   </details>

1. If you had Ansible Vault set up before, you'll need to create an [[Ansible Vault password file|Install: Ansible-Vault#password-file]] using the same vault password as last time.
   ```bash
   echo YOUR_VAULT_PASSWORD > /root/.ansible_vault
   ```
   of course, that should be your vault password, not literally YOUR_VAULT_PASSWORD.

1. Run [[preinstall|Install: Preinstall]] command to create a user account:

   ```bash
   cd ~/cloudbox
   sudo ansible-playbook cloudbox.yml --tags preinstall
   ```

   _Note: It's ok to do this in root as it will create a new user account and move the cloudbox folder and config files to that new user's home folder._

   **_Now log out of your `root` session and log in as the user account from your `accounts.yml` file._**

1. Run the restore command:

   _Note: Do not run this command while logged in as `root`.  Log in as your user account; the account you specified in `accounts.yml`_

   ```bash
   cd ~/cloudbox
   sudo ansible-playbook cloudbox.yml --tags restore
   ```
  
   _Note: If you are getting an error, verify that you are not logged in as root.  You should be logged in as the user account specified in `accounts.yml`.._

   _Note: If you are getting an error for rclone such as `permission denied` reboot the system then sign in as your user then run the restore tag again._

    That error will include: `... Failed to open log file: open /root/cloudbox/restore_rclone.log: permission denied", ...`

   _If you get an error related to a misconfigured rclone.conf file, check that file and make sure things look normal. Also run rclone config to check that a remote has actually been configured._


1. Install the relevant Cloudbox type: [[Cloudbox|Install: Cloudbox]], [[Mediabox|Install: Mediabox]], or [[Feederbox|Install: Feederbox]]. Example below.

   _Note: Do not run this command while logged in as `root`.  Log in as your user account; the account you specified in `accounts.yml`_

   Example:
   ```bash
   sudo ansible-playbook cloudbox.yml --tags cloudbox
   ```

1. Reboot.

1. If you had any extra, or non-default, containers previously (e.g [Community Roles](https://github.com/Cloudbox/Community)), you can install those now.

All applications, and their data, will now be restored.