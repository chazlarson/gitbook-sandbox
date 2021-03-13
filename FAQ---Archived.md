These are FAQs that are now obsolete to do some fixes/tweaks and are just here for archiving purposes.

- [Cloudbox Installer](#cloudbox-installer)
	- ["No package matching 'unrar' is available" ](#no-package-matching-unrar-is-available)
	- [Misc SSL Errors During Install](#misc-ssl-errors-during-install)
	- [apt-get Gets Stuck at 0% Because of IPv6](#apt-get-gets-stuck-at-0-because-of-ipv6)
- [Cloudbox Backup](#cloudbox-backup)
   - [Error: File changed as we read it](#error-file-changed-as-we-read-it)
- [Plex](#plex)
	- [Missing Thumbnails in Plex (due to http/https redirect errors)](#missing-thumbnails-in-plex-due-to-httphttps-redirect-errors)
	- [Update WebTools](#update-webtools)
- [NZBHydra1](#nzbhydra1)
  - [Error 502](#error-502)


---
# Cloudbox Installer

## "No package matching 'unrar' is available"

**Update: Now taken care of by Ansible.**

---

<pre>
failed: [localhost] (item=[u'unrar', u'unzip', u'p7zip', u'curl', u'sqlite3',
u'vnstat', u'tree', u'lsof', u'man-db', u'ksmtuned', u'git', u'pwgen', u'rsync',
u'logrotate', u'htop', u'iotop', u'nload', u'fail2ban', u'ufw', u'ncdu', u'mc',
u'speedtest-cli', u'nethogs', u'nodejs-legacy', u'npm', u'glances', u'screen',
u'tmux', u'apache2-utils']) => {"changed": false, "item": ["unrar", "unzip",
"p7zip", "curl", "sqlite3", "vnstat", "tree", "lsof", "man-db", "ksmtuned",
"git", "pwgen", "rsync", "logrotate", "htop", "iotop", "nload", "fail2ban",
 "ufw", "ncdu", "mc", "speedtest-cli", "nethogs", "nodejs-legacy", "npm",
"glances", "screen", "tmux", "apache2-utils"],
"msg": "No package matching 'unrar' is available"}
</pre>

  1. Edit the Common Task role:

      ```
      nano ~/cloudbox/roles/common/tasks/main.yml
      ```

  1. Replace `unrar` with `unrar-free` under the `Install common packages` section (below `with_items:`)

      ```
      - name: Install common packages
         apt: "name={{item}} state=installed"
         with_items:

      ```
  1. `Ctrl-x`, `y`, and `enter` to save.

  1. Retry setup.


## Misc SSL Errors during Install

**Update: Fixed with [[Dependencies Installer Script|Install: Dependencies#1-install-dependencies]]**

---

Example:
```
An exception occurred during task execution. To see the full traceback, use -vvv. The error was: AttributeError: 'module' object has no attribute 'Cryptography_HAS_SSL_ST'
```

This seems to occur on certain VM systems.

To fix it the issue, run the following command:

```
sudo easy_install pyOpenSSL

```


## apt-get Gets Stuck at 0% Because of IPv6

**Update: Now taken care of by the [[Dependencies Installer Script|Install: Dependencies#1-install-dependencies]].**

---

Example:
```
Get:65 http://mirror.hetzner.de/ubuntu/packages xenial-updates/multiverse amd64 Packages [16.2 kB]
Get:66 http://mirror.hetzner.de/ubuntu/packages xenial-updates/multiverse i386 Packages [15.3 kB]
Get:67 http://mirror.hetzner.de/ubuntu/packages xenial-updates/multiverse Translation-en [8,076 B]
Get:68 http://mirror.hetzner.de/ubuntu/security xenial-security/main amd64 Packages [472 kB]
Get:69 http://mirror.hetzner.de/ubuntu/security xenial-security/main i386 Packages [424 kB]
Get:70 http://mirror.hetzner.de/ubuntu/security xenial-security/main Translation-en [204 kB]
Get:71 http://mirror.hetzner.de/ubuntu/security xenial-security/restricted amd64 Packages [7,224 B]
Get:72 http://mirror.hetzner.de/ubuntu/security xenial-security/restricted i386 Packages [7,224 B]
Get:73 http://mirror.hetzner.de/ubuntu/security xenial-security/restricted Translation-en [2,152 B]
Get:74 http://mirror.hetzner.de/ubuntu/security xenial-security/universe amd64 Packages [340 kB]
Get:75 http://mirror.hetzner.de/ubuntu/security xenial-security/universe i386 Packages [297 kB]
Get:76 http://mirror.hetzner.de/ubuntu/security xenial-security/universe Translation-en [127 kB]
Get:77 http://mirror.hetzner.de/ubuntu/security xenial-security/multiverse amd64 Packages [3,208 B]
Get:78 http://mirror.hetzner.de/ubuntu/security xenial-security/multiverse i386 Packages [3,376 B]
Get:79 http://mirror.hetzner.de/ubuntu/security xenial-security/multiverse Translation-en [1,408 B]
0% [Connecting to security.ubuntu.com (2001:67c:1360:8001::21)]
```

Run this command:
``` bash
echo 'Acquire::ForceIPv4 "true";' | sudo tee /etc/apt/apt.conf.d/99force-ipv4
```

Retry install.

# Cloudbox Backup

## Error: File changed as we read it

**Update: File changes are now ignored during the tar creation task.**

---


When backup occurs, it shut's down all running Docker containers and apps. If you were to start them before backup completed and something was modified within the /opt folder, you'd get a message like this:

```
fatal: [localhost]: FAILED! => {"changed": true, "cmd": "tar --exclude='./plex/Library/Application Support/Plex Media Server/Cache/PhotoTranscoder' --ignore-failed-read -cf '/home/seed/Backups/Cloudbox/Feeder/cloudbox.tar' -C /opt .", "delta": "0:06:15.552758", "end": "2018-05-22 13:06:43.735333", "msg": "non-zero return code", "rc": 1, "start": "2018-05-22 13:00:28.182575", "stderr": "tar: ./radarr: file changed as we read it", "stderr_lines": ["tar: ./radarr: file changed as we read it"], "stdout": "", "stdout_lines": []}

```

If this occurs, simply rerun the backup again. You may need to start up the docker containers manually after it completes (run `docker ps -a` to see what containers are still stopped).



# Plex

## Missing Thumbnails in Plex (due to http/https redirect errors)

**Update: This has been added to Cloudbox as default config. Just [[update Cloudbox|Updating Cloudbox]] and [[reinstall nginx proxy|Updating Cloudbox Apps]]**

---

~~_A recent update to Plex AND/OR nginx-proxy has resulted in an issue where Plex decides to try and load item posters from http via port 443. This behavior is limited to Android clients, as iOS and Web clients work perfectly fine. It is unsure which piece of software is at fault here, be it nginx-proxy or most likely Plex. However, a temporary fix is provided below._~~



~~1. Go into the folder:~~

   ```
   cd ~/cloudbox
   ```
~~1. Edit the nginx-role~~
   ```
   nano roles/nginx-proxy/tasks/main.yml
   ```

~~1. Change `image:` info~~

  ~~ Replace ...~~
   ```
   image: "jwilder/nginx-proxy"
   ```

   ~~With ...~~
   ```
   image: "jwilder/nginx-proxy@sha256:76d9ed11c131fadc7546e3b9b085970e13ff45186171b975ad60830f5ca0d689"
   ```

~~1. Save the file: `Ctrl-X` + `Y`.~~

~~1. Recreate the nginx-proxy container~~

   ```
   sudo ansible-playbook cloudbox.yml --tags nginx-proxy
   ```


## Update WebTools

**Update: Now auto-updated with the Plex role.**

---


1. Remove your current WebTools.bundle folder.

   ```
   rm -rf "/opt/plex/Library/Application Support/Plex Media Server/Plug-ins/WebTools.bundle"
   ```

2. Update the Plex container

   ```
   cd ~/cloudbox
   sudo ansible-playbook cloudbox.yml --tags plex
   ```

3. Access Webtools

   ```
   http://plex.yourdomain.com:33400 (or http://youripaddress:33400)
   ```

# NZBHydra1

## Error 502

**Update:** The role takes care of this now - just reinstall NZBHydra.

---


NZBHydra v1 Suitarr to NZBHydra v1 LSIO Transition:

1. Stop NZBHydra: `docker stop nzbhydra`.

2. Backup previous folder: `mv /opt/nzbhydra/ /opt/nzbhydrav1_bak/`

3. `cd ~/cloudbox` + `git pull`

4. `sudo ansible-playbook cloudbox.yml --tags nzbhydra`

5.  After a minute: docker stop nzbhydra

6.  `rm /opt/nzbhydra/hydra/*`

7. Run these commands:

```
cp /opt/nzbhydrav1_bak/nzbhydra.db /opt/nzbhydra/hydra/
cp /opt/nzbhydrav1_bak/nzbhydra.db-shm /opt/nzbhydra/hydra/
cp /opt/nzbhydrav1_bak/nzbhydra.db-wal /opt/nzbhydra/hydra/
cp /opt/nzbhydrav1_bak/nzbhydra.cfg /opt/nzbhydra/hydra/settings.cfg
```

8. start nzbhydra: `docker start nzbhydra`

9. Enjoy!
