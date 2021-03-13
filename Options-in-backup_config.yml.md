## Notes

- `yes` and `no` can be interchanged with `true` and `false`, respectively.


## Config

- **local**

   - `enable` 

     - `yes` - Keep only the most recent backup locally.

     - `no` - Don't keep any backups locally.

     - Default is `yes`.

  - `desination` 

     - Path for local backups (tarballs). 

     - Default is `/mnt/local/Backups/Cloudbox`.


- **rclone**

   - `enabled` 
 
     - Enable/disable cloud backups. 

     - Options are `yes` or `no`. 

     - Default is `yes`.

  - `desination`

    - Path for cloud backups (e.g. Google Drive). Older backups are stored in the `archived` folder. 

    - If you use a Feederbox/Mediabox setup, you may want to change your paths to `google:/Backups/Feederbox` and `google:/Backups/Mediabox`, respectively.

    - Default is `google:/Backups/Cloudbox`.


- **rsync**

   - `enabled`

     - Enable/disable Rsync backups. 

     - Options are `yes` or `no`. 

     - Default is `no`.

  - `desination`

    - Path for Rsync backups. Only the most recent backup is kept.

- **cron**

  - `cron_time`

    - How often to backup should run (when `cron_state` is set to `present`). 

    - Options are: `reboot`, `yearly`, `annually`, `weekly`, `daily`, `hourly`. 

    - Default is `weekly`.

  - `cron_state`

    - Enable/disable automatic backups. 

    - Options are `absent` or `present`. Default is `absent`.

      - If you want cloudbox to **enable** automatic backups, enter `present`

      - If you want cloudbox to **disable** automatic backups, enter `absent`

      - Think of it as telling cloudbox "Leave automatic backups in this state."

- **restore service** 


  - Uploads config files to [[Cloudbox Restore Service|FAQ#what-is-cloudbox-restore-service]]. 

  - To enable, simply fill the login credentials you want to use.

    - NOTE: These are 'credentials` that *you are making up right now*; they do not need to [and *should not*] match any other user/pass [like your cloudbox user/pass].  They are used *only* for the [[Cloudbox Restore Service|FAQ#what-is-cloudbox-restore-service]], and the only entity that uses them is *you*.

  - For more details, see [[here|FAQ#what-is-cloudbox-restore-service]].

  - `user`

    - Username for Restore Service.

    - Tip: Use something like `domain.com` or `feederbox.domain.com`/`mediabox.domain.com` for easy to remember username. 

    - Note: This username is hashed on the client-side and never sent to the Restore Service in raw format.

  - `pass`

    - Password for Restore Service.


- **misc** 


  - Misc options.

  - `snapshot`

    - Enable / Disable snapshot support. 

    - Benefit: Docker containers are only stopped for a short period of time while snapshots are made.

    - Requires: BTRFS on `/opt` or `/`

    - Options are `true` or `false`. 

    - Default is `true`.
