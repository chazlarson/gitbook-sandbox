
- Each time the Cloudbox Installer runs, the Settings Updater checks to see if new updates are to be added to your config files (i.e. `accounts.yml`, `settings.yml`, and `adv_settings.yml`). 

- This allows new features and variable changes to be added directly into your settings file so that Cloudbox continues to function properly.

- When a new entry is added, the install will then immediately exit (as a FAIL) and show this message:


      TASK [settings : Check 'settings-updater.py' run status for new settings] **********************************************************************************************************************************************************
      Tuesday 01 May 2018  14:54:42 +0200 (0:00:00.019)       0:00:03.900 ***********
      fatal: [localhost]: FAILED! => {"changed": false, "failed": true, "msg": "The script 'settings_updater.py' added new settings. Check `settings-updater.log` for details of new setting names added."}
             to retry, use: --limit @/home/seed/cloudbox/cloudbox.retry

      PLAY RECAP *************************************************************************************************************************************************************************************************************************
      localhost                  : ok=8    changed=1    unreachable=0    failed=1



- User can then take a look at their config files or the `settings_updater.log` file to see what was added.

- After reviewing and making any necessary changes to the config file, the user can re- un the Cloudbox install.


