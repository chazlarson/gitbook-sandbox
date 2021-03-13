(work in progress)

```yaml
---
local:
  keep_local_copy: true
  destination: /home/{{user}}/Backups/
rclone:
  enabled: false
  destination: google:/Backups
rsync:
  enabled: false
  dest: rsync://somehost.com/Backups
cron:
  cron_time: weekly
  cron_state: absent
restore_service:
  user:
  pass:
```


- `backup`:

  - `tar_dest`: Path for local backups (.tar). Only the most recent backup is kept. Default is `/home/{{user}}/Backups`.

    - Note: Ensure the path does NOT have a trailing slash (` / `) or else backup will fail (i.e. `/sample/path`, but not `/sample/path/`).

  - `rsync_dest`: Path for rsync backups (.tar). Only the most recent backup is kept.

    - Note: Ensure the path does NOT have a trailing slash (` / `) or else backup will fail (i.e. `/sample/path`, but not `/sample/path/`).

  - `rclone_dest`: Path for cloud backups (e.g. Google Drive). Older backups are stored in the `archived` folder. Default is `google:/Backups`.

    - Note: Ensure the path does NOT have a trailing slash (` / `) or else backup "could" fail (i.e. `/sample/path`, but not `/sample/path/`).

  - `keep_local_copy`: Option to save local copies of the backup file in `tar_dest` after backup is complete. Default is `true`.

  - `use_rsync`: Option to enable/disable rsync backups. Options are `true` or `false`. Default is `false`.

  - `use_rclone`: Option to enable/disable cloud (i.e Google Drive) backups. Options are `true` or `false`. Default is `false`.

  - `cron_time`: How often to backup should run (only when `cron_state` is set to `present`). Options are `reboot`, `yearly`, `annually`, `weekly`, `daily`, or `hourly`. Default is `weekly`.

    - Note: It is not recommended to schedule backups hourly as backing up may take a long time and cause future backup attempts to fail (the backup will not occur while another one is in progress, thanks to backup.lock file being created/removed during this process).

  - `cron_state`: Option to enable/disable automatic backups. Options are `absent` or `present`. Default is `absent`.

    - `absent` will remove any existing backup schedule.

    - `present` will ensure it is always scheduled.

    - Note 1: Whenever this option is changed (e.g. `absent` to `present`; `present` to `absent`), a manual backup (`sudo ansible-playbook cloudbox.yml --tags backup`) must be run once in order to enable or disable the backup schedule.

    - Note 2: This option just allows Cloudbox to schedule the backup for you. You can also setup scheduled backups by creating root cron tasks.

  - `pushover_app_token`: Pushover App Token. Enables notifications to be sent when a backup task starts and finishes (requires both the `pushover_app_token` and the `pushover_user_key`). Default is blank.

  - `pushover_user_key`: Pushover User Key. Enables notifications to be sent when a backup task starts and finishes (requires both the `pushover_app_token` and the `pushover_user_key`). Default is blank.
